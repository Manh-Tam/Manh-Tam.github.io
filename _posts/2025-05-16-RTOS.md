---
layout: post
title: "Bài viết thứ 2"
date: 2025-05-16
---
Simple queue trong RTOS (ví dụ như FreeRTOS) là một cấu trúc dữ liệu dùng để truyền dữ liệu giữa các task hoặc giữa ISR và task theo cách FIFO (First-In, First-Out).

✅ Mục đích:
Giao tiếp an toàn giữa các task.

Truyền dữ liệu từ ISR đến task.

Tránh dùng biến dùng chung và tranh chấp tài nguyên (race conditions).

📦 Đặc điểm chính:
Đặc điểm	Mô tả
FIFO	Phần tử được thêm vào trước sẽ được lấy ra trước
Thread-safe	Tự động xử lý đồng bộ hóa giữa các task
Có thể dùng trong ISR	Với phiên bản xQueueSendFromISR() và xQueueReceiveFromISR()

🔧 Ví dụ với FreeRTOS:
#include "FreeRTOS.h"
#include "queue.h"

QueueHandle_t xQueue;

void SenderTask(void *pvParameters) {
    int valueToSend = 100;

    for (;;) {
        xQueueSend(xQueue, &valueToSend, portMAX_DELAY);
        vTaskDelay(pdMS_TO_TICKS(500));
    }
}

void ReceiverTask(void *pvParameters) {
    int receivedValue;

    for (;;) {
        if (xQueueReceive(xQueue, &receivedValue, portMAX_DELAY) == pdPASS) {
            // Xử lý dữ liệu nhận được
        }
    }
}

int main(void) {
    xQueue = xQueueCreate(10, sizeof(int)); // Tạo queue chứa tối đa 10 phần tử kiểu int

    xTaskCreate(SenderTask, "Sender", 128, NULL, 1, NULL);
    xTaskCreate(ReceiverTask, "Receiver", 128, NULL, 1, NULL);

    vTaskStartScheduler();
}
📌 Một số hàm thường dùng:
Hàm	Mô tả
xQueueCreate()	Tạo hàng đợi mới
xQueueSend()	Gửi phần tử vào queue (từ task)
xQueueReceive()	Nhận phần tử từ queue
xQueueSendFromISR()	Gửi từ ISR
xQueueReceiveFromISR()	Nhận từ ISR
