---
layout: post
title: Default Event Loop
published: true
date: 2019-11-18
categories: [esp32]
tags: [firmware]
comments: true
featured_img: "https://lh5.googleusercontent.com/r2VZHv66DFxY6YH2TGLOocmtjaVwD8J7FvUxEpfLurxKExmoNBhMHr4MgcyKCK8UmAmcqkpwjXMzj67G8hwZbjrKDkYZvo4bllsBP3YrULr-zuZIqPoXUqKZAmZlBLVdw9Hv7spq"
sitemap:
  lastmod: 2022-04-18
  priority: 0.5
  changefreq: 'monthly'
---

ESP-IDF has an **Event Loop** Library . This Library allows you to create an Event Loop and declare Events to which other components of your code can register handlers. Handler is a function which gets executed when a particular event occurs.

A default Event loop is already prepared by the IDF; it is responsible for generating major events like

- WIFI_EVENT
- IP_EVENT
- IP_EVENT_STA_GOT_IP

You only need to call a function which will create the default event loop .

After that you don’t have to create/run any freertos task to run the default event loop . the default Loop runs internally

You can register to the **default event loop** for events like WIFI_EVENT and handle the event according to your needs . You can also create your own events and post them to the default event loop . Other code components of yours can register by the events created by you.

In this way the default event loop can generate/dispatch major system Events as well as user-created ones . I guess This is sufficient for most of the application design , but if you really need an event loop other than the default you can create one , but then you will also have to run it by a freeRtos Task.

To distinguish between default & User event loop the API provided by the **esp_event** library is slightly different for both the cases

| **Default Event Loops**         | **User Event Loops**                |
| ------------------------------- | ----------------------------------- |
| esp_event_loop_create_default() | esp_event_loop_create()             |
| esp_event_loop_delete_default() | esp_event_loop_delete()             |
| esp_event_handler_register()    | esp_event_handler_register_with()   |
| esp_event_handler_unregister()  | esp_event_handler_unregister_with() |
| esp_event_post()                | esp_event_post_to()                 |

**EVENTS**

An Event consists of 2 identifiers

- The Event Base
- The Event ID

There can be multiple event ID under 1 Event Base

![](https://lh5.googleusercontent.com/r2VZHv66DFxY6YH2TGLOocmtjaVwD8J7FvUxEpfLurxKExmoNBhMHr4MgcyKCK8UmAmcqkpwjXMzj67G8hwZbjrKDkYZvo4bllsBP3YrULr-zuZIqPoXUqKZAmZlBLVdw9Hv7spq)


The **esp_event** library has Macros to declare and define events

Now we will follow the following example code to know how to use the default event loop

<https://github.com/espressif/esp-idf/tree/master/examples/system/esp_event/default_event_loop>

In The example a timer is made using **esp_timer** API and 3 event sources are created related to the timer. The events are

- An event is generated when timer is raised
- An event is generated when timer period expires
- An event is generated when the time is stopped

first declare Event in the **event_source.h** header file

```c
// event_source.h
// Declare an event base
ESP_EVENT_DECLARE_BASE(TIMER_EVENTS); // declaration of the timer events family

enum {               // declaration of the specific events under the timer event family
    TIMER_EVENT_STARTED,       // raised when the timer is first started
    TIMER_EVENT_EXPIRY,        // raised when a period of the timer has elapsed
    TIMER_EVENT_STOPPED        // raised when the timer has been stopped
};
```

Then define the event in **main.c** implementation file

```c
/* Event source periodic timer related definitions */
ESP_EVENT_DEFINE_BASE(TIMER_EVENTS);
```

Create the default event loop as
```c
// Create the default event loop
ESP_ERROR_CHECK(esp_event_loop_create_default());
```

To register an Event to the default event loop we have to use the following function

```c
esp_err_t esp_event_handler_register(
esp_event_base_t  event_base,
                  int32_t event_id,
                  esp_event_handler_t event_handler,
                  void* event_handler_arg
                );
```

For example to register **the event of timer start** the event base & Event ID is passed as follows

```c
// Register the specific timer event handlers.
ESP_ERROR_CHECK(esp_event_handler_register(
                                 TIMER_EVENTS, 
                                 TIMER_EVENT_STARTED, 
                                 timer_started_handler, 
                                 NULL));
```

To Post an Event to the default loop you have to use the following function . Remember you have to post your events to the default loop , default loop will then dispatch the event to the listening subscribers

```c
esp_err_t esp_event_post(
                    esp_event_base_t      event_base,
                    int32_t 			  event_id,
                    void* 			      event_data,
                    size_t 		          event_data_size,
                    TickType_t 		      ticks_to_wait
                    );
```

So the example code starts the timer and posts this very starting event to the default loop

```c
ESP_ERROR_CHECK(esp_timer_start_periodic(TIMER, TIMER_PERIOD));
ESP_ERROR_CHECK(esp_event_post(
                               TIMER_EVENTS, 
                               TIMER_EVENT_STARTED, 
                               NULL, 
                               0, 
                               portMAX_DELAY)
                               );
```

As soon as this event is got by the default loop , it dispatches the event to the corresponding handler which was registered before for this event

```c
// Handler which executes when the timer started event gets executed by the loop.
static void timer_started_handler(void* handler_args, esp_event_base_t base, int32_t id, void* event_data)
{
    ESP_LOGI(TAG, "%s:%s: timer_started_handler", base, get_id_string(base, id));
}
```

The handler basically prints a log about the event

So this is how you can use the default event loop to design an event driven application

**Reference**

<https://github.com/espressif/esp-idf/tree/master/examples/system/esp_event/default_event_loop>
