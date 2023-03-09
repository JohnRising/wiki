---
id: backup-restore
title: ব্যাকআপ / পুনরুদ্ধার নোড উদাহরণ
description: "একটি Polygon Edge নোড উদাহরণ ব্যাক আপ এবং পুনরুদ্ধার কিভাবে।"
keywords:
  - docs
  - polygon
  - edge
  - instance
  - restore
  - directory
  - node
---

## সংক্ষিপ্ত বিবরণ {#overview}

এই গাইড একটি Polygon Edge নোড উদাহরণ ব্যাক আপ এবং পুনরুদ্ধার কিভাবে উপর বিস্তারিত যায়। এটি বেস ফোল্ডার এবং তারা যা ধারণ করে, সেইসাথে একটি সফল ব্যাকআপ এবং পুনরুদ্ধার সম্পাদন জন্য ফাইল সমালোচক

## বেস ফোল্ডার {#base-folders}

Polygon Edge তার স্টোরেজ ইঞ্জিন হিসাবে লেভারেজ করে। একটি Polygon Edge নোড শুরু করার সময়, নিম্নলিখিত সাব-ফোল্ডার নির্দিষ্ট কাজ ডিরেক্টরি তৈরি করা হয়:
* **ব্লকচেইন** - ব্লকচেইন তথ্য
* চেষ্টা - **Merkle** চেষ্টা সংরক্ষণ (বিশ্ব রাষ্ট্র তথ্য)
* **keystore** - ক্লায়েন্ট জন্য ব্যক্তিগত কী এটি libp2p ব্যক্তিগত কী এবং sealing/validator ব্যক্তিগত কী
* **ঐক্যমত**্য - ক্লায়েন্ট কাজ করার সময় প্রয়োজন হতে পারে যে কোন ঐক্যমত্য তথ্য এখন, এটি নোডের *ব্যক্তিগত যাচাইকারী কী*

Polygon Edge উদাহরণ জন্য মসৃণ চালানোর জন্য এই ফোল্ডার সংরক্ষণ করা সমালোচক

## একটি চলমান নোড থেকে ব্যাকআপ তৈরি করুন এবং নতুন নোড জন্য পুনরুদ্ধার {#create-backup-from-a-running-node-and-restore-for-new-node}

এই বিভাগ একটি চলমান নোড ব্লকচেইন আর্কাইভ তথ্য তৈরি করে এবং অন্য উদাহরণ এটি পুনরুদ্ধার করার মাধ্যমে আপনাকে গাইড করে।

### ব্যাকআপ {#backup}

`backup`gRPC দ্বারা একটি চলমান নোড থেকে কমান্ড fetches ব্লক এবং একটি আর্কাইভ ফাইল কমান্ড `--from``--to`এবং না দেওয়া হয়, এই কমান্ড জেনেসিস থেকে সর্বশেষ ব্লক আনতে হবে।

```bash
$ polygon-edge backup --grpc-address 127.0.0.1:9632 --out backup.dat [--from 0x0] [--to 0x100]
```

### পুনরুদ্ধার {#restore}

পতাকা সঙ্গে শুরু করার সময় শুরু একটি আর্কাইভ থেকে একটি সার্ভার আমদানি ব্`--restore`লক। দয়া করে নিশ্চিত করুন যে নতুন নোড জন্য একটি কী আমদানি বা কী তৈরি সম্পর্কে আরও জানতে সি[ক্রেট ম্যানেজার অধ্যায়](/docs/edge/configuration/secret-managers/set-up-aws-ssm)

```bash
$ polygon-edge server --restore archive.dat
```

## ব্যাক আপ / পুরো তথ্য {#back-up-restore-whole-data}

এই বিভাগ রাষ্ট্র তথ্য এবং কী এবং নতুন উদাহরণ পুনরুদ্ধার সহ ডেটা ব্যাকআপ মাধ্যমে আপনাকে গাইড করে

### ধাপ 1: চলমান ক্লায়েন্ট {#step-1-stop-the-running-client}

যেহেতু Polygon Edge ডেটা স্টোরেজ জন্য **LevelDB** ব্যবহার করে, নোড ব্যাকআপ সময়কাল জন্য বন্ধ করা প্রয়োজন, **LevelDB** তার ডাটাবেস ফাইল সমতুল্য অ্যাক্সেস জন্য অনুমতি দেয় না।

উপরন্তু, Polygon Edge এছাড়াও বন্ধ তথ্য flushing করে।

প্রথম পদক্ষেপ চলমান ক্লায়েন্ট বন্ধ করা জড়িত (একটি সেবা ম্যানেজার বা প্রক্রিয়া একটি SIGINT সংকেত পাঠায় যে কিছু অন্যান্য প্রক্রিয়া মাধ্যমে), তাই এটি 2 ঘটনা ট্রিগার করতে পারে যখন gracefully নিচে শাট:
* ডিস্ক ডেটা ফ্লাশ
* LevelDB দ্বারা DB ফাইল লক

### ধাপ 2: ডিরেক্টরি {#step-2-backup-the-directory}

এখন ক্লায়েন্ট চলমান না হয়, তথ্য ডিরেক্টরি অন্য মাঝারি ব্যাক আপ করা যেতে পারে। একটি এক্সটেনশন সঙ্গে ফাইল `.key`ব্যক্তিগত কী তথ্য ধারণ করে এবং তারা একটি তৃতীয় / অজানা পার্টি সঙ্গে ভাগ করা

:::info
দয়া করে ব্যাকআপ `genesis`এবং ম্যানুয়ালি তৈরি ফাইল পুনরুদ্ধার করুন, তাই পুনরুদ্ধার নোড সম্পূর্ণরূপে অপারেশন
:::

## পুনরুদ্ধার {#restore-1}

### ধাপ 1: চলমান ক্লায়েন্ট {#step-1-stop-the-running-client-1}

Polygon Edge কোনো উদাহরণ চলমান হয়, এটি ধাপ 2 সফল হতে অর্ডার বন্ধ করা প্রয়োজন।

### ধাপ 2: পছন্দসই ফোল্ডার {#step-2-copy-the-backed-up-data-directory-to-the-desired-folder}

ক্লায়েন্ট চলমান না হলে, পূর্বে ব্যাক আপ ডেটা ডিরেক্টরি পছন্দসই ফোল্ডার কপি করা যেতে পারে। উপরন্তু, পূর্বে কপি `genesis`ফাইল

### ধাপ 3: সঠিক তথ্য ডিরেক্টরি নির্দিষ্ট করার সময় Polygon Edge ক্লায়েন্ট {#step-3-run-the-polygon-edge-client-while-specifying-the-correct-data-directory}

Polygon Edge পুনরুদ্ধার তথ্য ডিরেক্টরি ব্যবহার করার জন্য, আরম্ভ করতে, ব্যবহারকারী পথ নির্দিষ্ট করতে তথ্য ডিরেক্টরি। অনুগ্রহ করে [পতাকা সংক্রান্ত তথ্য CLI কমান্ড](/docs/edge/get-started/cli-commands) `data-dir`অধ্যায়