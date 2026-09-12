## Source Code

### Directory Structure

CHIP ၏ src directory ကို အောက်ပါအတိုင်း ဖွဲ့စည်းထားပါသည် −

| File / Folder | Contents                                           |
| ------------- | -------------------------------------------------- |
| app           | Application Layer -- Zigbee Cluster Library (ZCL)  |
| ble           | BLE Layer -- Bluetooth Transport Protocol (BTP)    |
| controller    | Controller API                                     |
| crypto        | Cryptography libraries                             |
| darwin        | Darwin Framework (iOS and macOS)                   |
| include       | Public headers                                     |
| inet          | Network Layer -- TCP and UDP endpoints             |
| lib           | Core and Support libraries                         |
| lwip          | Lightweight IP adaptation (to third_party library) |
| platform      | Device Layer -- platform portability adaptations   |
| qrcodetool    | QR code tool                                       |
| setup_payload | QR code setup data encode / decode library         |
| system        | System Layer -- common APIs for mem, work, etc.    |
| test_driver   | Framework for on-device testing                    |

#### Darwin

##### Near Field Communication Tag Reading

NFC Tag ဖတ်ခြင်းကို ဖွင့်ရန်အတွက် ငွေပေးချေထားသော Apple developer account လိုအပ်သောကြောင့် ၎င်းကို ပုံသေအားဖြင့် ပိတ်ထားပါသည်။ ၎င်းကို ဖွင့်လိုပြီး ငွေပေးချေထားသော Apple developer account ရှိပါက CHIPTool iOS target သို့ သွားပြီး Capabilities tab အောက်တွင် Near Field Communication Tag Reading ကို ဖွင့်ပါ။
