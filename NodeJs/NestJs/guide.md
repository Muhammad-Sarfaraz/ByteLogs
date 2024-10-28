# NestJs

# Buffer save to disk & Upload to AWS
```typescript
private async saveImageToDiskAndS3(imageUrl) {
    try {
      // Fetch the image as a buffer
      const response = await axios.get(imageUrl, { responseType: 'arraybuffer' });
      const imageBuffer = Buffer.from(response.data, 'binary');

      if (imageBuffer.length === 0) {
        throw new Error('Image buffer is empty');
      }

     const url = await this.awsService.uploadFile({ originalname: 'image.png', buffer: imageBuffer, mimetype: 'image/png' });
     console.log(url.Location)


      // Define the directory path
      const imagesDir = path.join(process.cwd(), 'public', 'images');

      // Create the directory if it doesn't exist
      if (!fs.existsSync(imagesDir)) {
        fs.mkdirSync(imagesDir, { recursive: true });
      }

      // Create the file name and full path
      const fileName = `image-${Date.now()}.png`;
      const filePath = path.join(imagesDir, fileName);

      // Save the image buffer to the file
      fs.writeFileSync(filePath, imageBuffer);

      console.log(`Image saved successfully at ${filePath}`);
      return filePath; // Return path or URL if needed
    } catch (error) {
      console.error('An error occurred while saving the image:', error);
      throw new InternalServerErrorException('Could not save image');
    }
  }
```

## Rate Limiting:
Install the ``` @nestjs/throttler ``` into the application.
```Bash
npm install --save @nestjs/throttler
```
``` AppModule.ts ```
```typescript
import { ThrottlerModule } from '@nestjs/throttler';

@Module({
  imports: [
    ThrottlerModule.forRoot({
      ttl: 60,
      limit: 100,
    }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```
``` BooksController.ts ```
```typescript
@Controller('books')
@UseGuards(ThrottlerGuard)
export class BookssController {
  // Code Here...
}

```
Override default configuration for Rate limiting and duration.
```typescript
  @UseGuards(ThrottlerGuard)
  @Throttle({ default: { limit: 3, ttl: 60000 } })
  @Get('books')
  sayHello(): string {
    return this.appService.books();
  }
```

## Decorator
Nest is built around a language feature called decorators. 

## Validation

#### File validation example:

```js
import {
  Controller,
  FileTypeValidator,
  Get,
  MaxFileSizeValidator,
  ParseFilePipe,
  Post,
  UploadedFile,
  UseGuards,
  UseInterceptors,
} from '@nestjs/common';
import { AwsService } from './aws.service';
import { CreateAwDto } from './dto/create-aw.dto';
import { UpdateAwDto } from './dto/update-aw.dto';
import { FileInterceptor } from '@nestjs/platform-express';
import { JwtAuthGuard } from 'src/auth/guards/jwt.auth.guard';

const MIME_TYPES = ['image/*', 'application/pdf'];

@Controller('aws')
export class AwsController {
  constructor(private readonly awsService: AwsService) {}

  @Post('upload')
  // @UseGuards(JwtAuthGuard)
  @UseInterceptors(FileInterceptor('file'))
  async uploadFile(
    @UploadedFile(
      new ParseFilePipe({
        validators: [
          new MaxFileSizeValidator({
            maxSize: 100000000,
            message: 'Validation failed (expected size is less than 100MB)',
          }),
          new FileTypeValidator({ fileType: '.(png|jpeg|jpg|pdf)' }),
        ],
      }),
    )
    file: Express.Multer.File,
  ) {
    try {
      const { Location } = await this.awsService.uploadFile(file);
      return {
        success: true,
        location: Location,
      };
    } catch (e) {
      console.log(e);
      return {
        success: false,
        message: 'Something went wrong. Please try again.',
      };
    }
  }
}

```
