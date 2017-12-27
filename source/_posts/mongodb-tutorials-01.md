---
title: "[MongoDB] 01.시작하기"
date: 2017-12-21 13:16:30
tags:
- Database
- NoSQL
categories:
- Database
- NoSQL
---
이 장에서는 MongDB의 기본적인 사용법을 정리합니다.
DB, Collection, Document의 생성 및 조회를 위한 기본 명령어를 소개합니다.


### DB 생성 & Collection 생성
MongoDB는 RDB와 같은 별도의 DB생성 명령이 존재하지 않는다. (ex. CREATE DATABASE ;)
`USE` 명령을 통해 사용할 DB를 선택하고 Collection 을 생성하면 DB는 자동으로 생성된다.
{% codeblock lang:javascript%}
// DB생성
use opera            // 실행
switched to db opera // 결과

// Collection 생성
// ex) db.createCollection('DB명', [옵션]);

// 실행
db.createCollection('shops');
// 결과
{ 
    "ok" : 1.0
}

// 데이터베이스 목록
show dbs

admin      0.000GB
config     0.000GB
homestead  0.000GB
local      0.000GB
opera      0.000GB
tests      0.000GB


// 현재 선택된 DB 확인
db

opera

// Collection 목록 확인
show collections

shops

{% endcodeblock %}

### Document 생성 & 조회
Document 생성은 단일 Insert와 Bulk Insert 각각 다른 결과를 Return 한다.
{% codeblock lang:javascript%}
// Insert Document
db.shops.insert({
  mall_id: "bpmt001",
  shop_no: 1,
  shop_name: "테스트몰(국문)",
  locale: "ko_KR",
  currency: "KRW"
})

WriteResult({ "nInserted" : 1 }) // 결과

// Bulk Insert
db.shops.insert([
    {
        mall_id: "bpmt001",
        shop_no: 2,
        shop_name: "테스트몰(영문)",
        locale: "en_US",
        currency: "USD"
    },
    {
        mall_id: "bpmt001",
        shop_no: 3,
        shop_name: "테스트몰(일문)",
        locale: "ja_JP",
        currency: "JPY"
    }
])

//결과
BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 2,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})

// 검색
db.shops.find()

// 결과
{ 
    "_id" : ObjectId("5a41f77b78cc2bf83d7b206e"), 
    "mall_id" : "bpmt001", 
    "shop_no" : 1.0, 
    "shop_name" : "테스트몰(국문)", 
    "locale" : "ko_KR", 
    "currency" : "KRW"
}
{ 
    "_id" : ObjectId("5a41f7ea78cc2bf83d7b206f"), 
    "mall_id" : "bpmt001", 
    "shop_no" : 2.0, 
    "shop_name" : "테스트몰(영문)", 
    "locale" : "en_US", 
    "currency" : "USD"
}
{ 
    "_id" : ObjectId("5a41f7ea78cc2bf83d7b2070"), 
    "mall_id" : "bpmt001", 
    "shop_no" : 3.0, 
    "shop_name" : "테스트몰(일문)", 
    "locale" : "ja_JP", 
    "currency" : "JPY"
}

// 조건검색
db.shops.find({locale: "ko_KR"})
// 결과
{ 
    "_id" : ObjectId("5a41f77b78cc2bf83d7b206e"), 
    "mall_id" : "bpmt001", 
    "shop_no" : 1.0, 
    "shop_name" : "테스트몰(국문)", 
    "locale" : "ko_KR", 
    "currency" : "KRW"
}
{% endcodeblock %}

# Document 수정
{% codeblock lang:javascript%}
// Field Update : 특정 필드의 값만 없데이트 하기
// 특정필드의 값을 수정할땐 $set 연산자를 사용합니다. 이 연산자를 사용해서 새로운 Field를 추가할 수도 있습니다.
db.shops.update(
	{locale: "ko_KR"},
	{
	  $set: {
	    shop_name: "테스트몰(국문) 2nd"
	  }
	}
)
// 결과
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

// Replace Document : Object의 ID값은 변경되지 않고 문서를 Replace 하기.
db.shops.update(
	{locale: "ko_KR"},
    { 
        "mall_id" : "bpmt001", 
        "shop_no" : 1.0, 
        "shop_name" : "테스트몰(국문) 2nd", 
        "locale" : "ko_KR", 
        "currency" : "KRW"
    }
)
// 결과
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

// 특정필드를 제거하기
db.shops.update(
	{locale: "ko_KR"},
    { 
      $unset: {"currency": 1}
    }
)
//결과
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

// criteria에 해당되는 document가 존재하지 않는다면 새로 추가하기
db.shops.update(
	{locale: "zh_CN"},
    { 
        mall_id: "bpmt001",
        shop_no: 4,
        shop_name: "테스트몰(중문)",
        locale: "zh_CN",
        currency: "CNY"
    },
    {upsert: true}
)
// 결과
WriteResult({
	"nMatched" : 0,
	"nUpserted" : 1,
	"nModified" : 0,
	"_id" : ObjectId("5a42006dc593ce3009ebeb1f")
})

// Document 여러개 수정하기
// multi 옵션을 true로 설정해야 조건에 맞는 여러개의 Document가 수정된다.
db.shops.update(
	{mall_id: "bpmt001"},
	{$set: {
	  service: ["translation"]
	}},
	{upsert: true, multi: true}
)

// 배열에 값 추가하기 + 오름차순 정렬하기
db.shops.update(
	{mall_id: "bpmt001"},
	{$push: {
	  service: {
	    $each: ["etc", "special"],
	    $sort: 1
	  }
	}},
	{multi: true}
)
// 결과
WriteResult({ "nMatched" : 3, "nUpserted" : 0, "nModified" : 3 })
// $sort 값이 1인경우 ASC, -1 인경우 DESC

// 배열에서 값 제거하기
db.shop.update(
	{mall_id: "bpmt001", shop_no: 2},
	{
	  $pull: {service: "etc"}
	}
)
// 결과
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })


// 배열에서 값 여러개 제거하기
db.shops.update(
    {mall_id: "bpmt001", shop_no: 2},
    {
        $pull: {
            service: {
                $in: ["etc", "special"]
            }
        }
    }
)

{% endcodeblock %}