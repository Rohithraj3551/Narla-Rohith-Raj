#include "stm32f7xx_hal.h"

// Example UART handle (adjust for your FC's hardware UART)
extern UART_HandleTypeDef huart2; // Use the UART port connected to camera

// MSP command to change camera settings (example: change brightness)
uint8_t msp_cmd[] = {
    0x24, 0x4D, 0x3C, // '$M<'
    0x05,             // Data length
    0x30,             // MSP command: CAMERA_SET
    0x01, 0x02, 0x03, 0x04, 0x05, // Example payload
    0xAB              // Checksum (calculate as needed)
};

void send_msp_command(void) {
    HAL_UART_Transmit(&huart2, msp_cmd, sizeof(msp_cmd), 100);
}

// Call this function when you want to configure camera
void configure_camera(void) {
    send_msp_command();
}
