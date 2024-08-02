# NestJs

#### Raw SQL Query

```js
import { Analytics } from './entities/analytics.entity';
import { Connection, Repository } from 'typeorm';
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';

@Injectable()
export class AnalyticsService {
  constructor(
    @InjectRepository(Analytics)
    readonly analyticsRepository: Repository<Analytics>,
    private readonly connection: Connection,
  ) {}
  
async analytics(){
  const rawQuery = `
  SELECT * from analytics join users on analytics.user_id = users.id;
`;
const result = await this.connection.query(rawQuery);

return result;
}
}
```
