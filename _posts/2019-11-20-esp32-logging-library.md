---
layout: post
title: Usage of Logging Library
published: true
date: 2019-11-20
categories: [esp32]
tags: [firmware]
comments: true
featured_img: "https://lh6.googleusercontent.com/PHPhdFsrfDD43mqFtvt9L7INpXMv1hqq8UJz7peqP_MU7PJkHXNTNNLH5S37ahWghSNUGJJvIxfM5NT-osQ5kykpEM-rManmdPdLfj_v5lrrxaRMRMWkKKpC1xMS7YvPd0EgUveQ"
sitemap:
  lastmod: 2022-04-18
  priority: 0.5
  changefreq: 'monthly'
---

ESP32 has a very convenient Logging Library

In arduino like projects Normally what we do is that we print out our debug information using Serial print function.

On the Other hand, Esp-idf logging library forces you to print debug/log messages in a constructive way so that later you can easily visualize the logs according to the debug type categories and module groups. If you have experience in Android Application development then you will find this library similar .

ESP-IDF has different Logging functions as listed below

| **type** | **MACRO type functions** | **Verbosity Level** |
| -------- | ------------------------ | ------------------- |
| Error    | ESP_LOGE(tag, format, …) | Lowest              |
| Warning  | ESP_LOGW(tag, format, …) |                     |
| Info     | ESP_LOGI(tag, format, …) |                     |
| Debug    | ESP_LOGD(tag, format, …) |                     |
| Verbose  | ESP_LOGV(tag, format, …) | Highest             |

So what you can do is that you can categorize your log messages into the above 5 groups according to your need.

- If you have an **information** log to print, use the ESP_LOGI() function.
- If you have a **warning** log to print use the ESP_LOGW() function

All the functions expect you to put a TAG of type character string .

Let's say you have written a kalman filter class by yourself and in this class you are going to print different types of debug messages. So before using the macro function to print the logs, create a TAG saying “Kalman'' . Then pass this TAG to all of the debug function calls. The ESP logging library will print these “Kalman” tagged debug messages with the TAG first so that you can easily distinguish these particular module logs, in addition you also get the warning/info/error kind of categorization . So if you follow this approach in all of your code modules then ultimately the debug dump gets very convenient to see.

```c
static const char\* TAG ="Kalman";   
ESP_LOGW(TAG,"threshold exceeded %d baud", error \*100);
ESP_LOGI(TAG,"filtering complete");
```

By default the CONFIG_LOG_DEFAULT_LEVEL is set to **info** level,

![](https://lh6.googleusercontent.com/PHPhdFsrfDD43mqFtvt9L7INpXMv1hqq8UJz7peqP_MU7PJkHXNTNNLH5S37ahWghSNUGJJvIxfM5NT-osQ5kykpEM-rManmdPdLfj_v5lrrxaRMRMWkKKpC1xMS7YvPd0EgUveQ)

which means that the logging statements whose verbosity levels are higher than **Info** level will be disabled . So if you use ESP_LOGD( ) or ESP_LOGV( ) functions , their message will not get printed

Surely you can change this using the menuconfig .

Now let’s say that you want to keep Error, Warning and Info type logging enabled throughout your total codebase but for your “kanman” class you want to log only the Error type messages . in this case you can use the following function

```c
esp_log_level_set("Kalman", ESP_LOG_ERROR); // enable till ERROR level
```

This function will set the logging level for the “Kanman” TAGGed module to ERROR level only . But the Other TAGGed module will follow the default level set by the CONFIG_LOG_DEFAULT_LEVEL macro .

**Reference**

<https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/system/log.html>

  
  
  
  
