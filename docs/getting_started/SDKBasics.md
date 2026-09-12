# SDK Architecture ခြုံငုံသုံးသပ်ချက်

## စတင်အသုံးပြုခြင်း

-   SDK တည်နေရာ:
    [https://github\.com/project\-chip/connectedhomeip](https://github.com/project-chip/connectedhomeip)\_
-   အခြား repo များသို့ ဝင်ရောက်ခွင့်ရရှိရန်နှင့် project\-chip org တွင် ထည့်သွင်းခံရရန်
    _[help@csa\-iot\.org](mailto:help@csa-iot.org)_ သို့ email ပို့ပါ

## အခြေခံ SDK Architecture

![](img/SDK_layers.png)

### Platform Layer

Platform layer သည် network stack နှင့် base OS သို့ ချိတ်ဆက်မှုကို implement လုပ်ဆောင်ပေးပါသည်။ Message များသည် wire ပေါ်မှ platform layer အတွင်းသို့ စီးဆင်းဝင်ရောက်လာပြီး၊ Matter stack မှ ပြုပြင်ရန်အတွက် platform API ထဲသို့ route ပြန်လှည့်ပေးပါသည်။

### Platform API

Platform API သည် core နှင့် အပြန်အလှန်ဆက်သွယ်ရန်အတွက် ဘုံအလွှာတစ်ခုကို သတ်မှတ်ပေးပါသည်။

### Core

Core သည် underlying communication protocol များ အားလုံးအပါအဝင် spec ၏ အစိတ်အပိုင်းအများအပြားကို ဖုံးအုပ်ထားပါသည်။ Core code ၏ ရည်ရွယ်ချက်မှာ cluster request နှင့် ဆက်စပ်သည့် endpoint အချက်အလက်ကို ညွှန်ပြသော valid message များကို ember layer သို့ ပို့ဆောင်ပေးရန် ဖြစ်ပါသည်။

### Ember

Ember layer သည် သီးခြား device တစ်ခုတည်း (ONE SPECIFIC device) ၏ composition ကို implement လုပ်ဆောင်ပေးသော generated layer တစ်ခု ဖြစ်ပါသည်။ ၎င်းသည် message တစ်ခုစီကို စစ်ဆေးကြည့်ပြီး ရွေးချယ်ထားသော endpoint ပေါ်ရှိ cluster ပေါ်တွင် ရွေးချယ်ထားသော attribute (သို့) command ကို device က implement လုပ်ထားခြင်း ရှိမရှိ ဆုံးဖြတ်ကာ၊ implementation နှင့် access control ပေါ်မူတည်၍ ပိတ်ဆို့ခြင်း (သို့) route ပြုလုပ်ခြင်း ဆောင်ရွက်ပေးပါသည်။

Valid ဖြစ်သော request များကို ကိုင်တွယ်ရန် cluster implementation များသို့ ပေးပို့ပြီး invalid request များကို error တစ်ခုနှင့်အတူ ပြန်ပို့ပါသည်။ Ember layer သည် သင့် device ကို သင့် device အဖြစ် ဖြစ်စေသော အစိတ်အပိုင်းပင် ဖြစ်ပါသည်။ အများစုကို zap ကို အသုံးပြု၍ static အနေနှင့် generate လုပ်ထားပါသည်။

### Cluster implementation များ

Cluster implementation များသည် cluster ၏ နောက်ကွယ်တွင်ရှိသော logic ဖြစ်ပါသည်။ Cluster implementation code သည် cluster ပေါ်တွင် data model operation များ (ဖတ်ခြင်း / ရေးသားခြင်း / command invoke ခြင်း) ကို တောင်းဆိုရန် ember layer မှ message များကို လက်ခံရရှိပါသည်။ ၎င်းတို့သည် event generation နှင့် attribute ပြောင်းလဲမှု reporting အတွက်လည်း တာဝန်ရှိပါသည်။ ရိုးရှင်းသော cluster logic ကို ember callback function များတွင် ရေးသားနိုင်သော်လည်း၊ ပိုမိုရှုပ်ထွေးသော cluster logic ကိုမူ run-time တွင် install လုပ်ထားသော interface layer များတွင် ကိုင်တွယ်ဆောင်ရွက်ပါသည်။

## SDK ဖွဲ့စည်းပုံ (အဓိကအချက်များ)

-   docs
    -   [docs/guides/BUILDING\.md](https://github.com/project-chip/connectedhomeip/blob/master/docs/guides/BUILDING.md) -
        ဦးစွာ ဤအရာကို လိုက်နာလုပ်ဆောင်ပါ
    -   [docs/guides/chip_tool_guide.md](https://github.com/project-chip/connectedhomeip/blob/master/docs/guides/chip_tool_guide.md)
-   examples
    -   [examples/chip-tool](https://github.com/project-chip/connectedhomeip/blob/master/examples/chip-tool) -
        အဓိက controller ဥပမာ
    -   [examples/all-clusters-app](https://github.com/project-chip/connectedhomeip/blob/master/examples/all-clusters-app) -
        QA app
    -   [examples/\<others\>](https://github.com/project-chip/connectedhomeip/blob/master/examples) -
        Device အသီးသီးအတွက် ဥပမာများ
-   scripts
    -   [bootstrap.sh](https://github.com/project-chip/connectedhomeip/blob/master/scripts/bootstrap.sh)
        &
        [activate.sh](https://github.com/project-chip/connectedhomeip/blob/master/scripts/activate.sh) -
        environment တပ်ဆင်ခြင်း
    -   [build/build_examples.py](https://github.com/project-chip/connectedhomeip/blob/master/scripts/build/build_examples.py) -
        ဥပမာ code ကို build လုပ်ခြင်း
    -   [tools/zap/run_zaptool.sh](https://github.com/project-chip/connectedhomeip/blob/master/scripts/tools/zap/run_zaptool.sh) -
        zap tool ကို စတင်ခြင်း
    -   [tools/zap_regen_all.py](https://github.com/project-chip/connectedhomeip/blob/master/scripts/tools/zap_regen_all.py) -
        .zap -> .matter
-   src
    -   [controller](https://github.com/project-chip/connectedhomeip/blob/master/src/controller/) -
        python implementation အပါအဝင် client ဘက်ခြမ်း code
    -   [app](https://github.com/project-chip/connectedhomeip/blob/master/src/app) -
        server ဘက်ခြမ်း အခြေခံ code
    -   [app/clusters](https://github.com/project-chip/connectedhomeip/blob/master/src/app/clusters) -
        cluster implementation များ (.cpp)
    -   [app/zap-templates/zcl/data-model/chip/](https://github.com/project-chip/connectedhomeip/blob/master/src/app/zap-templates/zcl/data-model/chip/) -
        cluster definition များ (.xml)
    -   [app/tests/suites/certification](https://github.com/project-chip/connectedhomeip/blob/master/src/app/tests/suites/certification) -
        yaml cert test automation script များ
    -   [lib/support/](https://github.com/project-chip/connectedhomeip/blob/master/src/lib/support/) -
        ဘုံသုံး utility များ၏ Embedded ဗားရှင်းများ
    -   [platform](https://github.com/project-chip/connectedhomeip/blob/master/src/platform) -
        platform delegate API / implementation များ
    -   [include/platform](https://github.com/project-chip/connectedhomeip/blob/master/src/include/platform) -
        platform delegate API / implementation များ
    -   [python_testing](https://github.com/project-chip/connectedhomeip/blob/master/src/python_testing) -
        python cert test automation script များ
-   zzz_generated/app-common/app-common/zap-generated/\*
    -   generate လုပ်ထားသော cluster logic / namespace အားလုံး
-   data_model
    -   ဤ file များကို generate လုပ်ထားခြင်းဖြစ်ပြီး spec နှင့် ကိုက်ညီမှုရှိမရှိ စစ်ဆေးရန်
        အသုံးပြုပါသည်။ ၎င်းတို့ကို ကိုယ်တိုင် ပြင်ဆင်ခြင်း မပြုသင့်ပါ။
