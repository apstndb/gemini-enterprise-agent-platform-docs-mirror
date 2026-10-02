---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication
title: Replicate voices
description: Learn how to replicate a speaker's voice from reference and consent audio and use it with the Gemini 3.8 TTS models on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

> To learn more, run the "Gemini 3.8 Flash TTS" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/audio/speech/getting-started/gemini_3_8_flash_tts.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Faudio%2Fspeech%2Fgetting-started%2Fgemini_3_8_flash_tts.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Faudio%2Fspeech%2Fgetting-started%2Fgemini_3_8_flash_tts.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/audio/speech/getting-started/gemini_3_8_flash_tts.ipynb)

You can reproduce the voice, tone, cadence, and timbre of a speaker from a short audio sample using the *voice replication* feature. Both [Gemini 3.8 Flash TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts) ( `gemini-3.8-flash-tts` ) and [Gemini 3.8 Flash-Lite TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts) ( `gemini-3.8-flash-lite-tts` ) support voice replication.

To replicate a voice, you send a reference recording of the speaker ( `source_audio` ) and a recording of the same speaker reading a consent statement ( `consent_audio` ) to the Voices API. The service verifies consent and returns an identifier for the replicated voice. You then pass that identifier in `speechConfig.voiceConfig.voice` in `generateContent` or `streamGenerateContent` requests, without uploading the audio again.

## Storage modes

When you create a replicated voice, the `store` field selects one of two storage modes:

  - **Stored voice ( `store: true` )** : Google stores the replicated voice in your project and returns a voice ID ( `voice_...` ) in the `id` field. You can list, get, and delete stored voices with the Voices API.
  - **Voice replication key ( `store: false` )** : Google doesn't store the replicated voice. The service returns an encrypted voice replication key ( `voicekey_...` ) in the `key` field, and your application stores the key. Use this mode if your workload requires that Google doesn't keep voice profiles.

| Storage mode                             | Identifier     | Management                                                 | Expiration            |
| :--------------------------------------- | :------------- | :--------------------------------------------------------- | :-------------------- |
| Stored voice ( `store: true` )           | `voice_...`    | Voices API `list` , `get` , and `delete` methods           | 1 year after last use |
| Voice replication key ( `store: false` ) | `voicekey_...` | Stored by your application. Google doesn't retain the key. | 7 days after creation |

Generating speech with a stored voice restarts its one-year retention period, so a voice that you use regularly doesn't expire. A request that uses an expired voice replication key fails with an `INVALID_ARGUMENT` error, and a request that uses a deleted or expired stored voice fails with a `NOT_FOUND` error. To keep using a replicated voice, create it again before it expires.

## Before you begin

Complete the steps in [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#before-you-begin) on the Gemini TTS page. The Voices API is available in the `global` location through the `v1beta1` API version.

## Audio and consent requirements

Each request to create a replicated voice needs two recordings of the same adult speaker:

  - **Reference audio ( `source_audio` )** : 10 to 30 seconds of clean, natural speech from the speaker whose voice you want to replicate. Longer samples generally produce better results.

  - **Consent audio ( `consent_audio` )** : A recording of the same speaker reading the consent statement for their language word for word. For the statements, see [Supported languages and consent statements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication#consent-statements) . In English, the statement is:
    
    > *"I am the owner of this voice and have consented to the creation of a synthetic model of my voice through the use of Google Cloud."*

Both recordings must be WAV files with 16-bit little-endian linear PCM, mono, at 24 kHz.

If the consent recording doesn't match the consent statement, or the audio doesn't meet the usage guidelines, the `create` request fails with an `INVALID_ARGUMENT` error that describes the problem.

## Create a stored replicated voice

Set the following fields in the request:

  - `store` : `true` .
  - `voice.type` : `VOICE_TYPE_REPLICATED` .
  - `voice.display_name` : Optional. A name for the voice.
  - `voice.replicated.source_audio` and `voice.replicated.consent_audio` : The base64-encoded reference and consent recordings, each with `mime_type` set to `audio/wav` .

Don't set `voice.model` . Requests that set a model together with `store: true` fail with an `INVALID_ARGUMENT` error.

The response returns the voice ID in the `id` field.

### Python

    import base64
    
    from google import genai
    
    client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")
    
    with open("SOURCE_AUDIO_PATH", "rb") as f:
        source_b64 = base64.b64encode(f.read()).decode("utf-8")
    
    with open("CONSENT_AUDIO_PATH", "rb") as f:
        consent_b64 = base64.b64encode(f.read()).decode("utf-8")
    
    replicated_voice = client.voices.create(
        store=True,
        voice={
            "type": "VOICE_TYPE_REPLICATED",
            "display_name": "Custom replicated speaker",
            "replicated": {
                "source_audio": {"mime_type": "audio/wav", "data": source_b64},
                "consent_audio": {"mime_type": "audio/wav", "data": consent_b64},
            },
        },
        timeout=60,
    )
    
    # The voice ID starts with "voice_".
    print(f"Created voice ID: {replicated_voice.id}")

### REST

    SOURCE_B64=$(base64 -w 0 SOURCE_AUDIO_PATH)
    CONSENT_B64=$(base64 -w 0 CONSENT_AUDIO_PATH)
    
    cat > request.json <<EOF
    {
      "store": true,
      "voice": {
        "type": "VOICE_TYPE_REPLICATED",
        "displayName": "Custom replicated speaker",
        "replicated": {
          "sourceAudio": {"mimeType": "audio/wav", "data": "${SOURCE_B64}"},
          "consentAudio": {"mimeType": "audio/wav", "data": "${CONSENT_B64}"}
        }
      }
    }
    EOF
    
    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices \
      -d @request.json | jq -r '.id'

Replace the following:

  - PROJECT\_ID : Your Google Cloud project ID.
  - SOURCE\_AUDIO\_PATH : The path to the reference WAV file.
  - CONSENT\_AUDIO\_PATH : The path to the consent WAV file.

To list, get, or delete stored replicated voices, use the same methods as for designed voices. For details, see [Manage stored voices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design#manage) .

## Create a voice replication key

Set the following fields in the request:

  - `store` : `false` .
  - `voice.type` : `VOICE_TYPE_REPLICATED` .
  - `voice.model` : Required. The Gemini 3.8 TTS model to create the key with, for example `gemini-3.8-flash-tts` . The key works with both Gemini 3.8 TTS models.
  - `voice.replicated.source_audio` and `voice.replicated.consent_audio` : The base64-encoded reference and consent recordings, each with `mime_type` set to `audio/wav` .

The response returns the voice replication key in the `key` field.

### Python

    import base64
    
    from google import genai
    
    client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")
    
    with open("SOURCE_AUDIO_PATH", "rb") as f:
        source_b64 = base64.b64encode(f.read()).decode("utf-8")
    
    with open("CONSENT_AUDIO_PATH", "rb") as f:
        consent_b64 = base64.b64encode(f.read()).decode("utf-8")
    
    replicated_voice = client.voices.create(
        store=False,
        voice={
            "model": "gemini-3.8-flash-tts",
            "type": "VOICE_TYPE_REPLICATED",
            "replicated": {
                "source_audio": {"mime_type": "audio/wav", "data": source_b64},
                "consent_audio": {"mime_type": "audio/wav", "data": consent_b64},
            },
        },
        timeout=60,
    )
    
    # Store the key in your application. It starts with "voicekey_".
    voice_key = replicated_voice.key

### REST

    SOURCE_B64=$(base64 -w 0 SOURCE_AUDIO_PATH)
    CONSENT_B64=$(base64 -w 0 CONSENT_AUDIO_PATH)
    
    cat > request.json <<EOF
    {
      "store": false,
      "voice": {
        "model": "gemini-3.8-flash-tts",
        "type": "VOICE_TYPE_REPLICATED",
        "replicated": {
          "sourceAudio": {"mimeType": "audio/wav", "data": "${SOURCE_B64}"},
          "consentAudio": {"mimeType": "audio/wav", "data": "${CONSENT_B64}"}
        }
      }
    }
    EOF
    
    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices \
      -d @request.json | jq -r '.key'

## Generate speech with a replicated voice

Pass the voice ID or the voice replication key in `speechConfig.voiceConfig.voice` :

### Python

    from google import genai
    
    client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")
    
    response = client.models.generate_content(
        model="gemini-3.8-flash-tts",
        contents=[{
            "role": "user",
            "parts": [{
                "text": "Hello! This audio was generated with a replicated voice.",
                "speech_metadata": {"style": "warm and conversational"},
            }],
        }],
        config={
            "response_modalities": ["AUDIO"],
            "speech_config": {"voice_config": {"voice": "VOICE"}},
        },
    )
    
    # The SDK has already decoded the base64 audio, so inline_data.data is a
    # complete WAV file by default.
    with open("replicated_voice.wav", "wb") as f:
        f.write(response.candidates[0].content.parts[0].inline_data.data)

### REST

    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-tts:generateContent \
      -d '{
        "contents": [{
          "role": "user",
          "parts": [{
            "text": "Hello! This audio was generated with a replicated voice.",
            "speechMetadata": {"style": "warm and conversational"}
          }]
        }],
        "generationConfig": {
          "responseModalities": ["AUDIO"],
          "speechConfig": {
            "voiceConfig": {"voice": "VOICE"}
          }
        }
      }' | jq -r '.candidates[0].content.parts[0].inlineData.data' | base64 --decode > replicated_voice.wav

Replace VOICE with the voice ID ( `voice_...` ) or the voice replication key ( `voicekey_...` ) that the `create` method returned.

Voice creation requests are subject to a per-project, per-minute quota. If you exceed it, the `create` method returns a `RESOURCE_EXHAUSTED` error. For more information, see [Quotas and system limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas) .

## Supported languages and consent statements

The Voices API verifies consent by matching the transcript of `consent_audio` against the consent statement. The speaker must read the statement for their language word for word:

| Language          | BCP-47 code | Consent statement                                                                                                                                   |
| :---------------- | :---------- | :-------------------------------------------------------------------------------------------------------------------------------------------------- |
| Afrikaans         | `af`        | Ek is die eienaar van hierdie stem en het ingestem tot die skep van 'n sintetiese model van my stem deur die gebruik van Google Cloud.              |
| Albanian          | `sq`        | Unë jam pronari i këtij zëri dhe kam dhënë pëlqimin për krijimin e një modeli sintetik të zërit tim përmes përdorimit të Google Cloud.              |
| Amharic           | `am`        | የዚህ ድምጽ ባለቤት እኔ ነኝ እና የጉግል ክላውድን በመጠቀም የድምፄ ሰው ሰራሽ ሞዴል እንዲፈጠር ተስማምቻለሁ።                                                                              |
| Arabic            | `ar`        | أنا صاحب هذا الصوت وقد وافقت على إنشاء نموذج اصطناعي لصوتي باستخدام خدمة جوجل كلاود.                                                                |
| Armenian          | `hy`        | Ես այս ձայնի սեփականատերն եմ և համաձայնություն եմ տվել Google Cloud-ի միջոցով իմ ձայնի սինթետիկ մոդելի ստեղծմանը։                                   |
| Azerbaijani       | `az`        | Mən bu səsin sahibiyəm və Google Cloud vasitəsilə səsimin sintetik modelinin yaradılmasına razılıq vermişəm.                                        |
| Bangla            | `bn`        | আমি এই কণ্ঠস্বরের মালিক এবং গুগল ক্লাউড ব্যবহারের মাধ্যমে আমার কণ্ঠস্বরের একটি কৃত্রিম মডেল তৈরিতে সম্মতি দিয়েছি।                                  |
| Basque            | `eu`        | Ahots honen jabea naiz eta nire ahotsaren eredu sintetiko bat sortzeko baimena eman dut Google Cloud erabiliz.                                      |
| Belarusian        | `be`        | Я з'яўляюся ўладальнікам гэтага голасу і даў згоду на стварэнне сінтэтычнай мадэлі майго голасу з дапамогай Google Cloud                            |
| Bulgarian         | `bg`        | Аз съм собственикът на този глас и съм дал съгласието си за създаването на синтетичен модел на моя глас чрез използването на Google Cloud.          |
| Burmese           | `my`        | ကျွန်ုပ်သည် ဤအသံ၏ပိုင်ရှင်ဖြစ်ပြီး Google Cloud ကိုအသုံးပြုခြင်းဖြင့် ကျွန်ုပ်၏အသံ၏ ပေါင်းစပ်ပုံစံတစ်ခု ဖန်တီးရန် သဘောတူပါသည်။                      |
| Catalan           | `ca`        | Sóc el propietari d'aquesta veu i he donat el meu consentiment per a la creació d'un model sintètic de la meva veu mitjançant l'ús de Google Cloud. |
| Cebuano           | `ceb`       | Ako ang tag-iya niining tingog ug miuyon sa paghimo og sintetikong modelo sa akong tingog pinaagi sa paggamit sa Google Cloud.                      |
| Chinese, Mandarin | `cmn`       | 我是这段声音的所有者，并已同意通过 Google Cloud 创建我的声音合成模型。                                                                                                          |
| Croatian          | `hr`        | Vlasnik sam ovog glasa i pristao sam na izradu sintetičkog modela mog glasa putem Google Clouda.                                                    |
| Czech             | `cs`        | Jsem vlastníkem tohoto hlasu a souhlasil(a) jsem s vytvořením syntetického modelu mého hlasu pomocí služby Google Cloud.                            |
| Danish            | `da`        | Jeg ejer denne stemme og har givet samtykke til oprettelsen af en syntetisk model af min stemme ved hjælp af Google Cloud.                          |
| Dutch             | `nl`        | Ik ben de eigenaar van deze stem en heb toestemming gegeven voor het creëren van een synthetisch model van mijn stem via Google Cloud.              |
| English           | `en`        | I am the owner of this voice and have consented to the creation of a synthetic model of my voice through the use of Google Cloud                    |
| Estonian          | `et`        | Olen selle hääle omanik ja olen andnud nõusoleku oma hääle sünteetilise mudeli loomiseks Google Cloudi abil.                                        |
| Filipino          | `fil`       | Ako ang may-ari ng boses na ito at pumayag sa paglikha ng isang sintetikong modelo ng aking boses sa pamamagitan ng paggamit ng Google Cloud.       |
| Finnish           | `fi`        | Olen tämän äänen omistaja ja olen antanut suostumukseni synteettisen ääneni mallintamiseen Google Cloudin avulla.                                   |
| French            | `fr`        | Je suis propriétaire de cette voix et j'ai consenti à la création d'un modèle synthétique de ma voix grâce à l'utilisation de Google Cloud.         |
| Galician          | `gl`        | Son o propietario desta voz e dei o meu consentimento para a creación dun modelo sintético da miña voz mediante o uso de Google Cloud.              |
| Georgian          | `ka`        | მე ვარ ამ ხმის მფლობელი და დავთანხმდი ჩემი ხმის სინთეზური მოდელის შექმნას Google Cloud-ის გამოყენებით.                                              |
| German            | `de`        | Ich bin der Inhaber dieser Stimme und habe der Erstellung eines synthetischen Modells meiner Stimme mithilfe von Google Cloud zugestimmt.           |
| Greek             | `el`        | Είμαι ο κάτοχος αυτής της φωνής και έχω συναινέσει στη δημιουργία ενός συνθετικού μοντέλου της φωνής μου μέσω της χρήσης του Google Cloud.          |
| Gujarati          | `gu`        | હું આ અવાજનો માલિક છું અને ગૂગલ ક્લાઉડના ઉપયોગ દ્વારા મારા અવાજનું સિન્થેટિક મોડેલ બનાવવા માટે સંમતિ આપી છે.                                        |
| Haitian Creole    | `ht`        | Mwen se pwopriyetè vwa sa a epi mwen bay konsantman pou kreyasyon yon modèl sentetik vwa mwen atravè itilizasyon Google Cloud.                      |
| Hebrew            | `he`        | אני הבעלים של קול זה והסכמתי ליצירת מודל סינתטי של קולי באמצעות Google Cloud.                                                                       |
| Hindi             | `hi`        | मैं इस आवाज का स्वामी हूं और मैंने Google क्लाउड के उपयोग के माध्यम से अपनी आवाज का कृत्रिम मॉडल बनाने की सहमति दी है।                              |
| Hungarian         | `hu`        | Én vagyok a hang tulajdonosa, és hozzájárultam ahhoz, hogy a Google Cloud segítségével szintetikus modellt készítsenek a hangomról.                 |
| Icelandic         | `is`        | Ég er eigandi þessarar raddar og hef samþykkt að búið sé til tilbúið líkan af rödd minni með því að nota Google Cloud.                              |
| Indonesian        | `id`        | Saya adalah pemilik suara ini dan telah menyetujui pembuatan model sintetis suara saya melalui penggunaan Google Cloud.                             |
| Italian           | `it`        | Sono il proprietario di questa voce e ho acconsentito alla creazione di un modello sintetico della mia voce tramite l'utilizzo di Google Cloud.     |
| Japanese          | `ja`        | 私はこの音声の所有者であり、Google Cloud を利用して私の音声の合成モデルを作成することに同意しました。                                                                                           |
| Javanese          | `jv`        | Aku sing nduwèni swara iki lan wis sarujuk kanggo nggawé model sintetis swaraku liwat panggunaan Google Cloud.                                      |
| Kannada           | `kn`        | ನಾನು ಈ ಧ್ವನಿಯ ಮಾಲೀಕ ಮತ್ತು Google Cloud ಬಳಕೆಯ ಮೂಲಕ ನನ್ನ ಧ್ವನಿಯ ಸಂಶ್ಲೇಷಿತ ಮಾದರಿಯನ್ನು ರಚಿಸಲು ಸಮ್ಮತಿಸಿದ್ದೇನೆ.                                           |
| Korean            | `ko`        | 저는 이 음성의 소유자이며, Google Cloud를 사용하여 제 음성의 합성 모델을 생성하는 데 동의했습니다.                                                                                      |
| Lao               | `lo`        | ຂ້ອຍເປັນເຈົ້າຂອງສຽງນີ້ ແລະ ໄດ້ຍິນຍອມໃຫ້ສ້າງຮູບແບບສັງເຄາະສຽງຂອງຂ້ອຍຜ່ານການນຳໃຊ້ Google Cloud                                                         |
| Latin             | `la`        | Huius vocis dominus sum et consensi sum ad creandum exemplar syntheticum vocis meae per usum Google Cloud.                                          |
| Latvian           | `lv`        | Esmu šīs balss īpašnieks un esmu piekritis sintētiska manas balss modeļa izveidei, izmantojot Google Cloud.                                         |
| Lithuanian        | `lt`        | Esu šio balso savininkas ir sutikau, kad naudojant „Google Cloud“ būtų sukurtas sintetinis mano balso modelis.                                      |
| Luxembourgish     | `lb`        | Ech sinn de Besëtzer vun dëser Stëmm an hunn der Erstellung vun engem synthetesche Modell vu menger Stëmm mat Hëllef vu Google Cloud zougestëmmt.   |
| Macedonian        | `mk`        | Јас сум сопственик на овој глас и се согласив за создавање синтетички модел на мојот глас преку користење на Google Cloud.                          |
| Malagasy          | `mg`        | Izaho no tompon'ity feo ity ary nanaiky ny hamorona modely sentetika amin'ny feoko amin'ny alàlan'ny fampiasana ny Google Cloud.                    |
| Malay             | `ms`        | Saya pemilik suara ini dan telah bersetuju untuk penciptaan model sintetik suara saya melalui penggunaan Google Cloud.                              |
| Malayalam         | `ml`        | ഈ ശബ്ദത്തിന്റെ ഉടമ ഞാനാണ്, Google ക്ലൗഡ് ഉപയോഗിച്ച് എന്റെ ശബ്ദത്തിന്റെ ഒരു സിന്തറ്റിക് മോഡൽ സൃഷ്ടിക്കാൻ ഞാൻ സമ്മതം നൽകിയിട്ടുണ്ട്.                  |
| Marathi           | `mr`        | मी या आवाजाचा मालक आहे आणि गूगल क्लाउडचा वापर करून माझ्या आवाजाचे कृत्रिम मॉडेल तयार करण्यास मी संमती दिली आहे.                                     |
| Mongolian         | `mn`        | Би энэ дуу хоолойны эзэмшигч бөгөөд Google Cloud ашиглан өөрийн дуу хоолойны синтетик загварыг бүтээхийг зөвшөөрсөн.                                |
| Nepali            | `ne`        | म यो आवाजको मालिक हुँ र गुगल क्लाउडको प्रयोग मार्फत मेरो आवाजको सिंथेटिक मोडेल सिर्जना गर्न सहमति दिएको छु।                                         |
| Norwegian, Bokmål | `nb`        | Jeg eier denne stemmen og har samtykket til at det opprettes en syntetisk modell av stemmen min ved bruk av Google Cloud.                           |
| Odia              | `or`        | ମୁଁ ଏହି ଭଏସ୍‌ର ମାଲିକ ଏବଂ Google Cloud ବ୍ୟବହାର ମାଧ୍ୟମରେ ମୋ ଭଏସ୍‌ର ଏକ ସିନ୍ଥେଟିକ୍ ମଡେଲ୍ ତିଆରି କରିବାକୁ ସମ୍ମତି ଦେଇଛି।                                    |
| Pashto            | `ps`        | زه د دې غږ مالک یم او د ګوګل کلاوډ په کارولو سره مې د خپل غږ د مصنوعي ماډل جوړولو ته رضایت ورکړی دی.                                                |
| Persian           | `fa`        | من مالک این صدا هستم و با ایجاد یک مدل مصنوعی از صدایم از طریق استفاده از Google Cloud موافقت کرده‌ام.                                              |
| Polish            | `pl`        | Jestem właścicielem tego głosu i wyraziłem zgodę na utworzenie syntetycznego modelu mojego głosu za pomocą Google Cloud                             |
| Portuguese        | `pt`        | Eu sou o proprietário desta voz e consinto com a criação de um modelo sintético da minha voz através do uso do Google Cloud.                        |
| Punjabi           | `pa`        | ਮੈਂ ਇਸ ਆਵਾਜ਼ ਦਾ ਮਾਲਕ ਹਾਂ ਅਤੇ ਗੂਗਲ ਕਲਾਉਡ ਦੀ ਵਰਤੋਂ ਰਾਹੀਂ ਆਪਣੀ ਆਵਾਜ਼ ਦੇ ਇੱਕ ਸਿੰਥੈਟਿਕ ਮਾਡਲ ਨੂੰ ਬਣਾਉਣ ਲਈ ਸਹਿਮਤੀ ਦਿੱਤੀ ਹੈ।                                |
| Romanian          | `ro`        | Sunt proprietarul acestei voci și am consimțit la crearea unui model sintetic al vocii mele prin utilizarea Google Cloud.                           |
| Russian           | `ru`        | Я являюсь владельцем этого голоса и дал согласие на создание синтетической модели моего голоса с использованием Google Cloud.                       |
| Serbian           | `sr`        | Ја сам власник овог гласа и пристао/ла сам на креирање синтетичког модела мог гласа коришћењем Google Cloud-а                                       |
| Sindhi            | `sd`        | مان هن آواز جو مالڪ آهيان ۽ گوگل ڪلائوڊ جي استعمال ذريعي پنهنجي آواز جي هڪ مصنوعي ماڊل جي تخليق تي رضامندي ڏني آهي.                                 |
| Sinhala           | `si`        | මම මෙම හඬෙහි හිමිකරු වන අතර Google Cloud භාවිතය හරහා මගේ හඬෙහි කෘතිම ආකෘතියක් නිර්මාණය කිරීමට කැමැත්ත පළ කර ඇත්තෙමි.                                |
| Slovak            | `sk`        | Som vlastníkom tohto hlasu a súhlasil/a som s vytvorením syntetického modelu môjho hlasu pomocou služby Google Cloud.                               |
| Slovenian         | `sl`        | Sem lastnik tega glasu in sem privolil v ustvarjanje sintetičnega modela mojega glasu z uporabo storitve Google Cloud.                              |
| Spanish           | `es`        | Soy el propietario de esta voz y he consentido la creación de un modelo sintético de mi voz mediante el uso de Google Cloud.                        |
| Swahili           | `sw`        | Mimi ndiye mmiliki wa sauti hii na nimekubali kuundwa kwa modeli ya sauti yangu iliyotengenezwa kwa njia ya Google Cloud.                           |
| Swedish           | `sv`        | Jag äger den här rösten och har samtyckt till att en syntetisk modell av min röst skapas med hjälp av Google Cloud.                                 |
| Tamil             | `ta`        | இந்தக் குரலின் உரிமையாளர் நானே, மேலும் கூகிள் கிளவுடைப் பயன்படுத்தி எனது குரலின் செயற்கை மாதிரியை உருவாக்குவதற்கும் நான் ஒப்புதல் அளித்துள்ளேன்.    |
| Telugu            | `te`        | ఈ స్వరానికి నేను యజమానిని మరియు గూగుల్ క్లౌడ్‌ను ఉపయోగించి నా స్వరం యొక్క కృత్రిమ నమూనాను రూపొందించడానికి నేను సమ్మతించాను.                         |
| Thai              | `th`        | ฉันเป็นเจ้าของเสียงนี้และได้ยินยอมให้สร้างแบบจำลองเสียงสังเคราะห์ของเสียงฉันโดยใช้ Google Cloud                                                     |
| Turkish           | `tr`        | Bu sesin sahibi benim ve Google Cloud kullanılarak sesimin sentetik bir modelinin oluşturulmasına izin verdim.                                      |
| Ukrainian         | `uk`        | Я є власником цього голосу та дав згоду на створення синтетичної моделі мого голосу за допомогою Google Cloud                                       |
| Urdu              | `ur`        | میں اس آواز کا مالک ہوں اور میں نے گوگل کلاؤڈ کے استعمال کے ذریعے اپنی آواز کا مصنوعی ماڈل بنانے پر رضامندی دی ہے۔                                  |
| Vietnamese        | `vi`        | Tôi là chủ sở hữu giọng nói này và đã đồng ý cho phép tạo ra một mô hình tổng hợp giọng nói của mình thông qua việc sử dụng Google Cloud.           |

## Best practices

  - **Record in a quiet environment** : Minimize echo, background noise, music, and overlapping voices. Output quality depends on the quality of `source_audio` .
  - **Match recording conditions** : Record `source_audio` and `consent_audio` with the same microphone in the same room so that speaker verification succeeds.
  - **Convert to the required format** : Resample recordings to 24 kHz, mono, 16-bit PCM WAV before you encode them.
  - **Plan for renewal** : Voice replication keys are valid for seven days, and stored voices expire one year after they were last used. Keep the source and consent recordings, or a process to collect them, so that you can create the voice again before it expires.

## What's next

  - Create a custom voice from a text description with [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) .
  - Learn about turn-level styling, inline tags, and multi-speaker dialogue in [Generate speech with Gemini TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview) .
