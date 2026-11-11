// ESP32 gửi B (mT) và F (mN) qua USB (Serial) và Wi-Fi (WebSocket), đồng thời tự phát trang web.
// Cần cài thư viện "WebSockets" của Markus Sattler (Library Manager). Các thư viện khác có sẵn trong ESP32 core.
#include <WiFi.h>
#include <WebServer.h>
#include <WebSocketsServer.h>
#include "page.h"

#define TEST_MODE 1                 // 1: gửi số liệu giả để thử kết nối; 0: đọc cảm biến thật
const char* AP_NAME = "TuTruong-Lab";   // tên Wi-Fi do ESP32 phát ra (không cần Internet)
const char* AP_PASS = "12345678";       // tối thiểu 8 ký tự

WebServer http(80);                 // phát trang web tại http://192.168.4.1
WebSocketsServer ws(81);            // dữ liệu thời gian thực tại ws://192.168.4.1:81

// ===== SỬA HAI HÀM NÀY CHO ĐÚNG CẢM BIẾN CỦA NHÓM =====
// Ví dụ: cảm biến Hall tuyến tính (kiểu SS49E, cấp 3,3 V) nối vào chân ADC1; lấy V0 và độ nhạy từ datasheet.
const int PIN_BX = 34, PIN_BY = 35, PIN_BZ = 32, PIN_F = 33;
const float V0 = 1.65f;             // V khi B = 0
const float K_B = 0.0092f;          // V trên mỗi mT (độ nhạy)
const float K_F = 100.0f;           // mN trên mỗi V (hiệu chuẩn bằng quả cân rồi sửa)
float readB(int pin) { return (analogReadMilliVolts(pin) / 1000.0f - V0) / K_B; }   // mT
float readF() { return analogReadMilliVolts(PIN_F) / 1000.0f * K_F; }                // mN

void setup() {
  Serial.begin(115200);
  WiFi.softAP(AP_NAME, AP_PASS);
  http.on("/", []() { http.send_P(200, "text/html; charset=utf-8", PAGE); });
  http.begin();
  ws.begin();
}

void loop() {
  http.handleClient();
  ws.loop();
  static uint32_t t = 0;
  if (millis() - t < 100) return;   // 10 mẫu mỗi giây
  t = millis();
  float bx, by, bz, F;
#if TEST_MODE
  float s = millis() / 1000.0f;
  bx = 5 * sin(0.5f * s); by = 40 + 25 * sin(0.4f * s); bz = 3 * cos(0.3f * s); F = 2.0f + 0.5f * sin(0.4f * s);
#else
  bx = readB(PIN_BX); by = readB(PIN_BY); bz = readB(PIN_BZ); F = readF();
#endif
  char msg[96];
  snprintf(msg, sizeof(msg), "{\"Bx\":%.3f,\"By\":%.3f,\"Bz\":%.3f,\"F\":%.3f}", bx, by, bz, F);
  Serial.println(msg);              // USB (Web Serial)
  ws.broadcastTXT(msg);             // Wi-Fi (WebSocket)
}
