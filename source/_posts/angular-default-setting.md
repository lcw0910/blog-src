---
title: Angular 4 기본설정
date: 2017-10-12 14:07:35
tags:
- front-end
- angular
- typescript
categories:
- Development
- Front-End
- Angular
---
이 장에서는 Angular 및 관련 라이브러리 설치와 기본 환경설정에 대해 알아본다...

## Requirements
* NodeJS
* Npm

## Angular 4 설치하기
### AngularCLI (개발지원을 위한 Angular의 Command Line Interface)

## 라이브러리 설치하기

### Font-Awesome 설치하기
{% codeblock Terminal lang:Bash %}
npm install --save font-awesome angular-font-awesome
{% endcodeblock %}

app.module.ts


{% codeblock app.module.ts lang:TypeScript%}
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AngularFontAwesomeModule } from 'angular-font-awesome';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AngularFontAwesomeModule // 모듈추가
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
{% endcodeblock %}
