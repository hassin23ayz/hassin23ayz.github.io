---
layout: post
title: UART programming in ESP32
published: true
date: 2019-10-02
categories: [esp32]
tags: [firmware]
featured_img: "https://upload.wikimedia.org/wikipedia/commons/5/53/Blog-esp32-uart-setup.jpg"
sitemap:
  lastmod: 2022-05-06
  priority: 0.5
  changefreq: 'monthly'
---

In this post we will see how ESP32 UART peripheral can be programmed 

**UART** stands for Universal Asynchronous Receiver Transmitter 

- ESP32 has 3 UART controllers
- These controllers are connected to the GPIO matrix allowing you to assign the UART peripherals to any of the GPIO 
- Communication speed is upto 5 Mbps 
- All the 3 UART interfaces can be accessed by the DMA controller or directly by the CPU 

<img src="https://upload.wikimedia.org/wikipedia/commons/3/3b/Blog-esp32-uart-table.png" style="display: block; margin: 0 auto">

If you look closely you can see other than the usual TX RX lines there are RTS and CTS lines.

- _what are RTS / CTS lines ?_

RTS / CTS flow control mechanism is part of the RS232 Standard. These 2 Lines help Transmitter and receiver to alert each other before transmission taking place. 

- RTS means Request to Send
- CTS means Clear to Send 

You can read more on this here [flow-control](https://www.brainboxes.com/faq/what-is-rts--cts-hardware-flow-control-).

<br>
ESP32 UART provides hardware management of the CTS and RTS signal lines & the corresponding software flow control. 

Now Let's get into programming the UART peripheral 

_**Set ESP32 Default Console Output**_ 

Esp-sdk uses menuconfig to set different configurations for the chip

- By default UART0 is selected as the controller for the console output 
- The UART0 is mapped to GPIO01(TXD0) & GPIO3(RXD0) pins 

In the ESP32-devkit board these GPIO lines are connected to CP2101 USB-UART module. So whenever we use printf() in the code to print something the printf function is internally using UART0 peripheral. Additionally this UART0 is also used by the bootloader to print it’s debug log and take binary image from the host machine during the flash process 

If you open menuconfig in any of the example project you can see the default settings as 

```bash 
hassin@hassin-HP:~/esp/hello_world$ idf.py menuconfig
```
<img src="https://upload.wikimedia.org/wikipedia/commons/8/87/Blog-esp32-uart-menuconfig.png" style="display: block; margin: 0 auto">

<br>
_**Code go through**_ 

We will go through the **_esp-idf/examples/peripherals/uart/uart_echo_** [code-link](https://github.com/espressif/esp-idf/tree/master/examples/peripherals/uart/uart_echo)
 example to understand how we should use UART of ESP32 . this is a very basic project and does not use RTS CTS software flow control . 

In this project the code sets 2 GPIOs to work with the UART1 controller. Any data received at the UART1 controller is echoed back to the same UART controller i.e UART1

So you need to connect an USB-UART module to the UART1 based GPIO pins and open a terminal app in your host machine

First we have to create & set a uart_config_t structure type variable according to our need 

```c
    /* Configure parameters of an UART driver,
     * communication pins and install the driver */
    uart_config_t uart_config = {
        .baud_rate = 115200,
        .data_bits = UART_DATA_8_BITS,
        .parity    = UART_PARITY_DISABLE,
        .stop_bits = UART_STOP_BITS_1,
        .flow_ctrl = UART_HW_FLOWCTRL_DISABLE
    };
```
Then we have to set the structure to one of the 3 UART controllers

```c
uart_param_config(UART_NUM_1, &uart_config);
```

The following function sets the internal UART Signals to GPIO pins 

```c
uart_set_pin(UART_NUM_1, ECHO_TEST_TXD, ECHO_TEST_RXD, ECHO_TEST_RTS, ECHO_TEST_CTS);
```

Afterwards we install the UART driver using the folloiwng SDK API 

```c
esp_err_t uart_driver_install(
  uart_port_t uart_num, 
  int rx_buffer_size, 
  int tx_buffer_size, 
  int queue_size, 
  QueueHandle_t* uart_queue, 
  int intr_alloc_flags);
```
understanding the API parameters is important. The following table describes it 

| **Parameter type** | **Argument** | **Meaning** | 
| --- | --- | --- |
| **uart_port_t** uart_num | UART_NUM_1 | Set your Uart controller | 
| **int** rx_buffer_size | BUF_SIZE*2 | The RX buffer size | 
| **int** tx_buffer_size | 0 | If 0 then TX function will block task until all data is sent | 
| **int** queue_size | 0 |  | 
| **QueueHandle_t*** uart_queue | NULL | If used then a new queue handle is created to provide access to UART events | 
| **int** intr_alloc_flags | 0 | Related to interrupt | 

We call the function with proper values 
```c
uart_driver_install(UART_NUM_1, BUF_SIZE * 2, 0, 0, NULL, 0);
```

The following function is used to read bytes from the UART buffer. 

```c++
int uart_read_bytes(
  uart_port_t uart_num, 
  uint8_t* buf, 
  uint32_t length, 
  TickType_t ticks_to_wait);
```
```c
int len = uart_read_bytes(UART_NUM_1, data, BUF_SIZE, 20 / portTICK_RATE_MS);
```
Then to Send data to the UART port from a given buffer and length the code use this function

```c++
int uart_write_bytes(
  uart_port_t uart_num, 
  const char* src, 
  size_t size);
```

```c
uart_write_bytes(UART_NUM_1, (const char *) data, len);
```

As the UART driver's parameter **tx_buffer_size** is set to zero. This function will not return until all the data have been sent out. Otherwise, if the **tx_buffer_size** > 0, this function will return after copying all the data to tx ring buffer & later UART ISR will move data from the ring buffer to TX FIFO gradually.

<br>
_**Build & Flash**_

```bash
hassin@hassin-HP:~/esp/esp-idf/examples/peripherals/uart/uart_echo$ idf.py -p /dev/ttyUSB0 flash monitor
```

_**Connection**_
Connect the USB-UART module to the ESP32 board
<img src="https://upload.wikimedia.org/wikipedia/commons/5/53/Blog-esp32-uart-setup.jpg" style="display: block; margin: 0 auto">

Then open a Serial terminal app to send data to the UART1 controller , i have used Arduino IDE Serial terminal

<img src="https://upload.wikimedia.org/wikipedia/commons/e/ec/Blog-esp32-uart-debug.png" style="display: block; margin: 0 auto">

Now whatever you send will get echoed back to your serial terminal App 