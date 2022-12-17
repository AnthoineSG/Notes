# Api Nestjs

Framework back qui permet une mise en place d'un serveur nodejs/express en utilisant une methode POO

## src/article/dto/index

Principalement du CRUD

On y defint les **types** des information en entrer et en sortie

```js
import { Field, InputType, ObjectType } from "@nestjs/graphql";
import { Article } from "../models/article.model";

// Indique le type de donnée en entrer
@InputType()
export class ArticleCreateInput {
  // Pour la creation d'un input
  @Field(() => String) // On recupere le title de type string et qui retourne un string
  title: string;

  @Field(() => String) // une description de type string et qui retourne un string
  description: string;

  @Field(() => String) // ...
  image: string;
}

// Les données en sortie seront de type object
@ObjectType()
export class ArticleCreateOutput {
  @Field(() => Article) // L'object sera de type Article definie dans le model
  article: Article;
}

// Les données en sortie seront de type object
@ObjectType()
export class ArticleDeleteOutput {
  @Field(() => ID) // Apres la suppression d'un article on recupere sont id
  articleId: Article["id"];
}

// L'update extends le create il herite donc de toutes ses spec
@InputType()
export class ArticleUpdateInput extends ArticleCreateInput {}
```

## src/article/models/index

Definition du model de la base de données

Definition de tout les champs et de leur spec

```js
import { Field, ID, ObjectType } from "@nestjs/graphql";
import { Entity, Column, PrimaryGeneratedColumn, BaseEntity } from "typeorm";

@Entity() // Model entiter a schematiser par la bdd
@ObjectType() // indique que cest recuperable par graphql
export class Article extends BaseEntity {
  @Field(() => ID)
  @PrimaryGeneratedColumn("uuid") // defini comme une pk
  id: string;

  @Field(() => String)
  @Column()
  title: string;

  @Field(() => String)
  @Column()
  description: string;

  @Field(() => String)
  @Column()
  image: string;
}
```

## src/article/resolvers/index

Definition des fonctions et de leur utilisation

```js
import { Query } from '@nestjs/common';
import { Args, ID, Mutation, Resolver } from '@nestjs/graphql';
import { Article } from '../models/article.model';
import { ArticleCreateInput, ArticleCreateOutput } from '../dto/article-create.dto';
import { ArticleUpdateInput, ArticleUpdateOutput } from '../dto/article-update.dto';
import { ArticleDeleteOutput } from '../dto/article-delete.dto';
import { ArticlePaginationArgs } from '../dto/article-pagination.dto';
import { ArticleService } from '../article.service';

// Defini une class qui utilisera un certain objet et effectura des action en conséquent
@Resolver(Article)
export class ArticleMutationsResolver {
  // definition du constructeur et du service qu'il utilisera
  constructor(private readonly articleService: ArticleService) {}

  @Mutation(() => ArticleCreateOutput)
  async articleCreate(@Args('input') input: ArticleCreateInput) {
    return this.articleService.articleCreate(input);
  }

  @Mutation(() => ArticleUpdateOutput)
  async articleUpdate(
    @Args({ name: 'articleId', type: () => ID }) articleId: Article['id'],
    @Args('input') input: ArticleUpdateInput
  ) {
    return this.articleService.articleUpdate(articleId, input);
  }

  @Mutation(() => ArticleDeleteOutput)
  async articleDelete(
    @Args({ name: 'articleId', type: () => ID }) articleId: Article['id']
  ) {
    return this.articleService.articleDelete(articleId);
  }
}

@Resolver(Article)
export class ArticleQueriesResolver {
  constructor(private readonly articleService: ArticleService) {}

  @Query(() => [Article])
  async articlesPagination(@Args() args: ArticlePaginationArgs) {
    return this.articleService.articlesList(args);
  }
}
```

## src/article/article-service

Definition de la logique qui utilise les types, les models, et les services

```js
import { Repository } from 'typeorm';
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Article } from './models/article.model';
import { ArticleCreateInput, ArticleCreateOutput } from './dto/article-create.dto';
import { ArticleUpdateInput, ArticleUpdateOutput } from './dto/article-update.dto';
import { ArticleDeleteOutput } from './dto/article-delete.dto';

@Injectable()
export class ArticleService {
  constructor(
    @InjectRepository(Article)
    private readonly articleRepository: Repository<Article>
  ) {}

  async articleCreate(input: ArticleCreateInput): Promise<ArticleCreateOutput> {
    const newArticle = this.articleRepository.create(input);
    const article = await this.articleRepository.save(newArticle);
    return { article };
  }

  async articleUpdate(
    articleId: Article['id'],
    input: ArticleUpdateInput
  ): Promise<ArticleUpdateOutput> {
    const article = await this.articleRepository.findOneOrFail(articleId);
    article.title = input.title;
    article.description = input.description;
    article.image = input.image;
    await article.save();
    return { article };
  }

  async articleDelete(
    articleId: Article['id']
  ): Promise<ArticleDeleteOutput> {
    const article = await this.articleRepository.findOneOrFail(articleId);
    await article.remove();
    return { articleId };
  }
}
```

## src/article/article-module

Definition du module des articles

```js
import { Module } from "@nestjs/common";
import { TypeOrmModule } from "@nestjs/typeorm";
import { ArticleService } from "./article.service";
import { Article } from "./models/article.model";
import { ArticleMutationsResolver } from "./resolvers/article.mutations.resolver";
import { ArticleQueriesResolver } from "./resolvers/article.queries.resolver";

@Module({
  imports: [TypeOrmModule.forFeature([Article])],
  providers: [ArticleService, ArticleMutationsResolver, ArticleQueriesResolver],
})
export class ArticleModule {}
```
