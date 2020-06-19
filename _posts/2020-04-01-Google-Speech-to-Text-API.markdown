---
layout: post
title:  "Google Speech-to-Text API 분석"
date:   2020-04-01 02:00:00 +0900
categories: 음성처리
---

## Google Cloud Speech-to-Text 변환 및 화자 분할 분석

- 2019.6월 기준 Google Speech-to-Text API 서비스에 대한 검토자료 입니다.
- 워낙 빠른 속도로 API가 개선되고 있기 때문에 [공식 문서와 샘플 코드](https://cloud.google.com/speech-to-text/docs)를 참고해야 합니다.

1. 오디오 파일은 FLAC, LINEAR16(WAV) 등 몇 가지 타입만 지원 합니다.
2. Streaming 방식은 긴 오디오 파일에 대해서도 빠른 응답을 받을 수 있지만, 10M 파일 사이즈 제한이 있습니다. ([Google Cloud Speech-to-Text API Streaming example](https://github.com/sungalex/VoiceMagic/blob/master/2.google_streaming.ipynb) 참조)
3. Google Cloud Storage를 이용한 Long_Running 방식은 10M 이상의 긴 오디오 파일도 처리 할 수 있지만, 응답시간이 길고, Timeout이 발생할 수 있습니다. ([Google Cloud Speech-to-Text API Long_Running example](https://github.com/sungalex/VoiceMagic/blob/master/3.google_long_running_with_gcs.ipynb) 참조)
4. 화자 분리는 en-US, en-IN, es-ES 언어 만 지원합니다. ([Google Cloud Speech-to-Text API speaker_diarization (English only)](https://github.com/sungalex/VoiceMagic/blob/master/4.google_speaker_diarization_english.ipynb) 참조)
5. 2019.6월 현재 시점에 Google STT에서 지원하는 긴 오디오의 한국어 음성에 사용 가능한 솔루션은 Long_Running 방식(위 3번 항목) 입니다. (이 방법은 화자 분할은 지원 안됨)
6. 10M 이상의 긴 오디오 파일을 Streaming 방식으로 처리하기 위해서는, 오디오 파일을 10M 이하로 잘라서 처리하는 방법이 있습니다. ([Google Cloud Speech-to-Text API Streaming example](https://github.com/sungalex/VoiceMagic/blob/master/7.google_streaming_with_long_audio.ipynb) 참조, 결과를 text 파일로 저장하는 기능 포함)
7. Microphone Streaming API를 이용해서, 긴 파일을 실시간 Streaming 방식으로 처리하는 방법은 [Google Cloud Speech-to-Text API Microphone Streaming emulate](https://github.com/sungalex/VoiceMagic/blob/master/8.google_streaming_with_microphone_emulate.ipynb) 파일과 [Google STT Python functions](https://github.com/sungalex/VoiceMagic/blob/master/modules/google_stt.py) 코드를 참고하세요.

### Google Cloud Speech-to-Text Config 속성

- JSON representation : [google.cloud.speech.types.RecognitionConfig](https://cloud.google.com/speech-to-text/docs/reference/rest/v1/RecognitionConfig)
- encoding : 오디오 인코딩 방식(LINEAR16, FLAC 등), [Google 문서 Link](https://cloud.google.com/speech-to-text/docs/encoding?hl=ko)
- sample_rate_hertz : 오디오 샘플링 Rate(8000, 16000, 44100, 48000 등), [Wikipedia 문서 Link](https://ko.wikipedia.org/wiki/샘플링_레이트)
- language_code : 언어 코드 (한국어: 'ko-KR', 영어: en-US)
- enable_automatic_punctuation : 구두점(punctuation) 자동 추가(True or False)
- enable_word_time_offsets : 단어별 시작/종료 시간 정보(True or False)
- enable_speaker_diarization : 화자 분할 여부(True or False)
- diarization_speaker_count : 화자 분할 시 화자 숫자
- model : 텍스트 변환 모델(video, phone_call, command_and_search, default) 선택, [Google 문서 Link](https://cloud.google.com/speech-to-text/docs/transcription-model)
