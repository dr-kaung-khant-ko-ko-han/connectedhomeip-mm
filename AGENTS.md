# Matter SDK အတွက် AI Agent လမ်းညွှန်ချက်များ

ဤဖိုင်သည် Matter SDK codebase ပေါ်တွင် အလုပ်လုပ်နေသော AI agent များအတွက်
လမ်းညွှန်ချက်များနှင့် ညွှန်ကြားချက်များကို ပေးအပ်ထားပါသည်။

## အထွေထွေ မူများ

-   **When in Rome** (context နှင့်လိုက်လျောစွာ ပြုမူပါ): ပြင်ဆင်လျက်ရှိသော code ၏
    လက်ရှိ အသုံးများသည့် style ကို လိုက်နာကိုက်ညီအောင် ရေးပါ။ အသေးစိတ်ကို
    [docs/style/CODING_STYLE_GUIDE.md](docs/style/CODING_STYLE_GUIDE.md) တွင်
    ကြည့်ပါ။
-   **Atomicity (အပိုင်းလိုက် သီးခြားစီ ပြင်ဆင်ခြင်း):** အသေးစား၊ တစ်ဆင့်ချင်း
    တိုးမြှင့်ပြောင်းလဲမှုများ ပြုလုပ်ပါ။ Refactoring နှင့် feature အသစ်
    အကောင်အထည်ဖော်မှုကို ရောနှောမလုပ်ပါနှင့်။
-   **No Filler Names (အဓိပ္ပာယ်မဲ့ အမည်များ ရှောင်ကြဉ်ခြင်း):** "support"၊
    "common"၊ "helpers"၊ "util"၊ "core" ကဲ့သို့သော အမည်များကို ရှောင်ကြဉ်ပါ။
    တိကျသော အမည်များကို အသုံးပြုပါ။
-   **Error Handling (အမှားကိုင်တွယ်မှု):** မအောင်မြင်နိုင်သည့် operation
    များအတွက် standard return type အဖြစ် `CHIP_ERROR` ကို အသုံးပြုပါ။ error
    စစ်ဆေးခြင်းနှင့် ပျံ့နှံ့ခြင်းကို အတိုချုံးစွာ ဆောင်ရွက်ရန် `VerifyOrReturnError`
    နှင့် `ReturnErrorOnFailure` macro များကို ပိုမို ဦးစားပေး အသုံးပြုပါ။
-   အထူးသဖြင့် early return ဖြစ်ပေါ်ချိန်များတွင် resource များကို သင့်လျော်စွာ
    သန့်ရှင်းရေး ဆောင်ရွက်ကြောင်း သေချာစေပါ။ သန့်ရှင်းရေးအတွက် RAII pattern
    များကို အများအားဖြင့် ဦးစားပေး အသုံးပြုပါ။
-   **Logging (မှတ်တမ်းတင်ခြင်း):** logging အတွက် `ChipLog*` macro များ (ဥပမာ
    `ChipLogProgress`၊ `ChipLogError`၊ `ChipLogDetail`) ကို အသုံးပြုပါ။ log
    များကို module အလိုက် (ဥပမာ `AppServer`၊ `InteractionModel`) သင့်လျော်စွာ
    ခွဲခြားထားကြောင်း သေချာစေပါ။

## လျစ်လျူရှုမည့် Directory များ

ဖိုင်များ သို့မဟုတ် code pattern များကို ရှာဖွေသည့်အခါ၊ ရှင်းလင်းစွာ ရှာဖွေရန်
တောင်းဆိုထားခြင်း မဟုတ်ပါက အောက်ပါ directory များကို လျစ်လျူရှုပါ -

-   `third_party/` (ပြင်ပ dependency များ ပါဝင်သည်)
-   `out/` (build artifact များ ပါဝင်သည်)

## Code Review ညွှန်ကြားချက်များ

-   XML ဖိုင်များ၏ content သို့မဟုတ် cluster များအတွက် `.matter` content ကို
    comment မပေးပါနှင့်။
-   ဤ SDK သည် အပြောင်းအလဲ ဖြစ်နိုင်ပြီး contributor အားလုံးအတွက် မရရှိနိုင်သေးသည့်
    လုပ်ဆောင်ဆဲ Matter specification တစ်ခုကို အကောင်အထည်ဖော်ထားပါသည်။ အထူး tool
    သို့မဟုတ် skill တစ်ခုမှတစ်ဆင့် နောက်ဆုံးဗားရှင်းကို ရှင်းလင်းစွာ ရယူနိုင်ခြင်း
    _မရှိပါက_ Matter specification ကို မသိရှိကြောင်းနှင့် scope အပြင်ဘက်ဖြစ်ကြောင်း
    သတ်မှတ်ပါ။
-   code ဘာလုပ်နေသည်ကို ပြန်ပြောရုံမျှသာ ဖြစ်သည့် "pat on the back" ပုံစံ
    comment များကို ရှောင်ကြဉ်ပါ။ တိကျသော code တိုးတက်မှုများ အကြံပြုရန်
    အာရုံစိုက်ပါ။
-   အတိုချုံး ရေးပါ။ code ကို လိုအပ်သည်ထက် ပို၍ မရှင်းပြပါနှင့်။
-   ဖြစ်လေ့ရှိသော typo များကို ရှာဖွေပြီး ပြင်ဆင်ရန် အကြံပြုပါ။
-   whitespace သို့မဟုတ် formatting နှင့်ပတ်သက်၍ comment မပေးပါနှင့် (auto-formatter
    များက ကိုင်တွယ်ဆောင်ရွက်ပေးပါသည်)။
-   embedded development အတွက် ပြောင်းလဲမှုများကို ဤအတိုင်း review ပြုလုပ်ပါ -
    -   heap allocation အသုံးပြုမှုကို လျှော့ချပါ။
    -   resource အသုံးပြုမှု (RAM/Flash) ကို optimize ပြုလုပ်ပါ။
    -   code bloat ဖြစ်စေနိုင်သည့် ရှုပ်ထွေးသော template များကို သတိထားပါ။

## API တည်ငြိမ်မှု

Public API များတွင် ဤ tree အပြင်ဘက်မှ consumer များ ရှိလေ့ရှိသောကြောင့်၊
၎င်းတို့ကို ပြောင်းလဲခြင်း သို့မဟုတ် တိုးချဲ့ခြင်း ပြုလုပ်သည့်အခါ source
compatibility ကို ထည့်သွင်းစဉ်းစားရန် လိုအပ်ပါသည်။ Compatibility ကို
ချိုးဖျက်ခြင်းသည် လုံးဝ တားမြစ်ထားခြင်း မဟုတ်သော်လည်း၊ ကောင်းမွန်သော
အကြောင်းပြချက်ရှိမှသာ ပြုလုပ်သင့်ပါသည်။ Public နှင့် internal API များကြား
ရှင်းလင်းသော နယ်နိမိတ် မရှိပါ − ဧရိယာတစ်ခုတွင် compatibility မည်မျှ
အရေးပါသည်ဆိုသည်မှာ ပြင်ပ client များ အသုံးပြုနိုင်ခြေ မည်မျှရှိသည်ပေါ်နှင့် API
ကိုယ်တိုင် တည်ငြိမ်သည်ဟု သတ်မှတ်ခံရသလား သို့မဟုတ် ဖွံ့ဖြိုးဆဲ feature တစ်ခုနှင့်
သက်ဆိုင်သလားဆိုသည်ပေါ်တွင် မူတည်ပါသည်။

Compatibility သည် ဆုံးဖြတ်ချက်တစ်ခုကို လွှမ်းမိုးသည့်နေရာတွင်၊ ၎င်းကို comment
သို့မဟုတ် commit message တွင် မှတ်တမ်းတင်ထားပါ − ထိုသို့ မှတ်တမ်းတင်မထားပါက
တမင်တကာ ချိုးဖောက်ခြင်းနှင့် တမင်တကာ workaround ပြုလုပ်ခြင်း နှစ်ခုစလုံးသည်
မတော်တဆ ဖြစ်ရပ်များအဖြစ် ထင်ရလိမ့်မည်။

## API ဦးစားပေးချက်များ

-   pointer + size အုပ်စုများထက် `src/lib/support/Span.h` မှ `chip::Span` ကို
    ဦးစားပေး အသုံးပြုပါ။ `Span` ကို const reference အဖြစ်မဟုတ်ဘဲ value အဖြစ်
    ပို့ပါ (`string_view` တစ်ခုအဖြစ် သဘောထားပါ)
-   const char span များအတွက် `fromCharString` အစား `"foo"_span` (ဆိုလိုသည်မှာ
    `operator _span`) ကို အသုံးပြုပါ။
-   `chip::Optional` ထက် `std::optional` ကို ဦးစားပေးပါ။
-   string formatting အတွက် `snprintf` ကို အသုံးပြုသည့်အစား
    `src/lib/support/StringBuilder.h` မှ `StringBuilder` ကို ဦးစားပေးပါ။

## Coding Style (အဓိကအချက်များ)

အသေးစိတ်အချက်အလက် အပြည့်အစုံအတွက်
[docs/style/CODING_STYLE_GUIDE.md](docs/style/CODING_STYLE_GUIDE.md) ကို
ကြည့်ပါ။

-   **C++**: C++17 standard။
    -   POD integer type များအတွက် `<cstdint>` မှ fixed-width integer type
        များကို အသုံးပြုပါ။
    -   header များတွင် top-level `using namespace` ကို ရှောင်ကြဉ်ပါ။
    -   ဖိုင်-internal class/object များအတွက် anonymous namespace များကို
        အသုံးပြုပါ။
    -   core SDK တွင် heap allocation နှင့် auto-resizing container များကို
        ရှောင်ကြဉ်ပါ။
-   **Python**: Python 3.11 standard။
    -   public API များတွင် type hint များ အသုံးပြုပါ။
    -   public API များအတွက် docstring များ ထည့်သွင်းပါ။
-   control flow များ (ဥပမာ `if`၊ `while`၊ `for` စသည်) အတွက် တစ်ကြောင်းတည်း
    (one-liner) အသုံးပြုသည့်တိုင် `{}` bracket ကို _အမြဲတမ်း_ ထည့်သွင်းပါ။

## Testing (စမ်းသပ်ခြင်း)

-   unit testing မဖြစ်နိုင်သော (ဥပမာ platform-specific code) အခြေအနေမှလွဲ၍
    ပြောင်းလဲမှုအားလုံးအတွက် unit test များ လိုအပ်ပါသည်။
-   `src/python_testing` နှင့် `src/app/tests/suites` ရှိ မျှော်မှန်းထားသော
    failure များကို စစ်ဆေးအတည်ပြုသည့် test များသည် failure ကို အဘယ်ကြောင့်
    မျှော်မှန်းထားသည်ကို ရှင်းလင်းစွာ ဖော်ပြသင့်ပါသည်။ ဖြစ်နိုင်ပါက သက်ဆိုင်ရာ
    specification လိုအပ်ချက်များ၏ အနှစ်ချုပ်ကို ထည့်သွင်းပါ။

## ဗိသုကာဆိုင်ရာ ကန့်သတ်ချက်များ

### Code-Driven Cluster များ

Code-driven cluster များသည် `DefaultServerCluster` ကို base class အဖြစ်
အသုံးပြုသည့် `src/app/clusters` ရှိ implementation များ ဖြစ်ပါသည်။ ၎င်းတို့ကို
ဖွံ့ဖြိုးတိုးတက်အောင် ပြုလုပ်သည့်အခါ -

-   `ReadAttribute`၊ `WriteAttribute` နှင့် `InvokeCommand` တို့ကို API contract
    အရ ရှိပြီးသား path များအတွက်သာ ခေါ်ဆိုပါသည်။ path validity check များ
    ထည့်သွင်းခြင်း မပြုလုပ်ပါနှင့် − `Attributes` သို့မဟုတ် `AcceptedCommands`
    မှန်ကန်နေသရွေ့ ၎င်းတို့သည် code size ကို တိုးစေပြီး မလိုအပ်ဘဲ ထပ်နေပါသည်။
-   Ember API များနှင့် generate လုပ်ထားသော ZAP accessor များကို
    `CodegenIntegration` layer အပြင်ဘက်တွင် အသုံးမပြုရပါ။
    `CodegenIntegration.h/cpp` သည် generate လုပ်ထားသော configuration နှင့်
    code-driven cluster logic အကြား မှတ်တမ်းတင်ထားသော bridge ဖြစ်ပါသည်။ core
    cluster code တွင် `EmberAfStatus` ကဲ့သို့သော type များ သို့မဟုတ်
    `emberAfContainsServer`၊ `emberAfReadAttribute`၊ `emberAfWriteAttribute`
    ကဲ့သို့သော function များကို ရှောင်ကြဉ်ပါ။
-   ဖိုင်များ ထည့်သွင်းသည့်အခါ − codegen-specific ဖိုင်များသည်
    `app_config_dependent_sources.cmake/gni` တွင် ပါဝင်သင့်ပြီး၊ ကျန်အားလုံးသည်
    `BUILD.gn` တွင် ပါဝင်သင့်ပါသည်။ ဖိုင်တိုင်း (အထူးသဖြင့် header များ) ကို
    ၎င်းတို့အနက် တစ်ခုခုတွင် ဖော်ပြထားကြောင်း သေချာစေပါ − reference
    မပြုထားသော ဖိုင်များ မရှိသင့်ပါ။

### နမူနာ Application များ (မှတ်တမ်း ရှာဖွေတွေ့ရှိခြင်း)

ကိုးကားရည်ညွှန်း application များ (ဥပမာ `examples/all-devices-app` သို့မဟုတ်
စိတ်ကြိုက် simulator tool များ) ကို လုပ်ဆောင်ခြင်း သို့မဟုတ် ခွဲခြမ်းစိတ်ဖြာ
သည့်အခါ၊ code ပြင်ဆင်ခြင်း သို့မဟုတ် ထုတ်လုပ်ခြင်း မပြုလုပ်မီ ၎င်း application
၏ dynamic runtime Interaction Model၊ တိကျသော CLI parameter များနှင့်
အကြံပြုထားသော product baseline pattern များကို နားလည်ရန် ၎င်း application ၏
သီးသန့် `docs/` folder သို့မဟုတ် `ARCHITECTURE.md` ဖိုင်ကို အမြဲစစ်ဆေးကြည့်ရှုပါ။

## အသုံးများသော Command များ

command အများစုသည် activate ပြုလုပ်ထားသော environment တစ်ခု လိုအပ်ပါသည်။
agent harness ကို run မလုပ်မီ user သည် ၎င်းကို ပြုလုပ်ထားပြီး ဖြစ်နိုင်သလို
မထားနိုင်လည်း ဖြစ်နိုင်ပါသည် − `$PW_PROJECT_ROOT` ကို သတ်မှတ်ထားပါက
environment သည် active ဖြစ်နေပြီဟု ယူဆနိုင်ပါသည်။

### Environment Activate ပြုလုပ်ခြင်း

`scripts/run_in_build_env.sh` ကို အသုံးပြု၍ environment အတွင်း command
များကို run နိုင်ပါသည် −
`scripts/run_in_build_env.sh "command"`

တနည်းအားဖြင့် သင်၏ shell တွင် environment ကို activate ပြုလုပ်နိုင်ပါသည် −
`source scripts/activate.sh`

### Build နှင့် Test

-   **ရရှိနိုင်သော target များ စာရင်းပြပါ**:
    `scripts/run_in_build_env.sh "./scripts/build/build_examples.py targets"`
-   **Ninja ဖိုင်များ Generate ပြုလုပ်ပါ**:
    `scripts/run_in_build_env.sh "./scripts/build/build_examples.py --target linux-x64-tests-clang --quiet gen"`
-   **test အားလုံးကို Build ပြုလုပ်ပြီး run ပါ**:
    `scripts/run_in_build_env.sh "./scripts/build/build_examples.py --target linux-x64-tests-clang --quiet build"`
-   **သီးခြား test တစ်ခု run ပါ**:
    `scripts/run_in_build_env.sh "ninja -C out/linux-x64-tests-clang --quiet path/to/test:test_name.run"`

    -   ရှင်းလင်းသော ဥပမာ −
        `scripts/run_in_build_env.sh "ninja -C out/linux-x64-tests-clang src/app/clusters/occupancy-sensor-server/tests:TestOccupancySensingCluster.run"`
    -   Compile ခြင်းနှင့် run ခြင်းကို ခွဲထားနိုင်ပါသည် (ဥပမာ memory debugger
        တစ်ခုအောက်တွင် run နေပါက သို့မဟုတ် အခြား option များ သတ်မှတ်ရန်
        လိုအပ်ပါက):

            ```bash
            scripts/run_in_build_env.sh "ninja -C out/linux-x64-tests-clang src/app/clusters/occupancy-sensor-server/tests:TestOccupancySensingCluster"`
            ./out/linux-x64-tests-clang/tests/TestOccupancySensingCluster
            ```

### Common App များ Build ပြုလုပ်ခြင်း

-   **chip-tool** (Interactive commissioning tool):
    `scripts/run_in_build_env.sh "./scripts/build/build_examples.py --target linux-x64-chip-tool-clang --quiet build"`
-   **all-clusters-app** (features ကြွယ်ဝသော device simulator):
    `scripts/run_in_build_env.sh "./scripts/build/build_examples.py --target linux-x64-all-clusters-clang --quiet build"`
-   **all-devices-app** (features ကြွယ်ဝသော အခြား simulator တစ်ခု):
    `scripts/run_in_build_env.sh "./scripts/build/build_examples.py --target linux-x64-all-devices-clang --quiet build"`

## ဖွံ့ဖြိုးရေး အရင်းအမြစ်များ

-   [docs/guides/writing_clusters.md](docs/guides/writing_clusters.md)
-   [docs/guides/migrating_ember_cluster_to_code_driven.md](docs/guides/migrating_ember_cluster_to_code_driven.md)
-   [docs/testing/unit_testing.md](docs/testing/unit_testing.md)
-   [docs/testing/integration_tests.md](docs/testing/integration_tests.md)
