void initMain(void *argument)
{
  MX_USB_DEVICE_Init();
  GPIOA -> ODR |= GPIO_PIN_0;

GPIO_PIN_6, GPIO_PIN_RESET);
  //0x00 Read identity
  //0x01 Device status request
  //0x02 Device status ready
  //0x03 Bus status request
  //0x04 Bus status
  //0x06 DIAG read memory
  //0x07 DIAG write memory
  //0x08 Read coding data
  //0x09 Write coding data
  //0x15 Fuel Consuption
  //0x30 Selftest
  //0x31 Download test prog
  //0x32 run test prog
  //0x33 end test prog
  //0x34 hw test prog
  //0x40 Read Adjustment value
  //0x41 Write Adjustment value
  //0x42 Prog Adjustment value
  //0x43
  //0x44 Delete adaptive value
  //0x51 Prog steper motor address
  //0x52 Delete steper motor address
  //0x53 Read Manufacture data
  //0x54 Write Manufacture data

  //0x5B does some test
  //0x5C affects the Light Dimmer
  //0x5E affects the Light Dimmer


  //0x0C Vehicle Control

  //0x69 Read ZCS/FA
  //0x80 Read Crash TELEGRAM
  //0x81 Dekete Crash TELEGRAM
  //0x82 IKE Sensor status request
  //0x83 IKE Sensor status

  //0x90 Login
  //0x9D Power Down
  //0x9F Terminate Diagnostic mode

  //0xA0 diag ack
  //0xA1 diag busy
  //0xA2 diag rejected
  //0xFF diag not ack
  uint8_t tx_data[] = {0xD0, 0x04, 0x80, 0x30,0xB4};
  uint8_t tx_data2[] = {0x80,0x04, 0x30,0xB4};
  uint8_t tx_data3[] = {0x80,0x04, 0x9F,0x1B};

  //0x1C
  //uint16_t tx_len = sizeof(tx_data);
  uint32_t t_last_test_ts = 0;
  uint8_t tst=0x00;
  /* Infinite loop */


  for(;;)
  {
      if (HAL_GetTick()-t_last_test_ts >= 5000) {
                            if (tst==0) {
                  SoftUartPuts(0,tx_data2,4);
                  tst=1;
              } else {
                  SoftUartPuts(0,tx_data3,4);
                  tst=0;
              }

              t_last_test_ts=HAL_GetTick();
     }

      if (ibus_available() > 0 ){
               HAL_GPIO_TogglePin (GPIOE, GPIO_PIN_15);
               ibus_msg_t *msg=ibus_read_message();
               rawsend_u8(msg->ibusmessage,msg->length);
               ibus_msg_destroy(msg);
      }

      osDelay(10);
  }

}
