# NestJs

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
