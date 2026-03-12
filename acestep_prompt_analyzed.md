# ACE-Step 프롬프트 분석 리포트

## 1) 분석 범위
- 대상: `app/ACE-Step-1.5/examples/text2music/*.json` (총 200개)
- 분석 필드: `caption`, `lyrics`, `bpm`, `duration`, `keyscale`, `language`, `timesignature`
- 목적:
  - 장르/스타일 전체 목록 분류
  - 장르별 매핑표(빈도 + 대표 예제)
  - caption 문장의 음악 지시 방식(악기/음색/보컬/이펙트/구조) 분류
  - `lyrics` 내부 `[]` 지문(파트 지시어) 체계 분석

---

## 2) 메타 필드 통계

### 2-1. 언어 분포 (`language`)
| language | count |
|---|---:|
| en | 52 |
| zh | 51 |
| ja | 31 |
| ko | 21 |
| fr | 19 |
| de | 13 |
| es | 5 |
| pl | 3 |
| hu | 2 |
| he | 1 |
| ms | 1 |
| pt | 1 |

### 2-2. 박자 분포 (`timesignature`)
| timesignature | count |
|---|---:|
| 4 | 183 |
| 2 | 9 |
| 3 | 8 |

### 2-3. BPM / Duration
- BPM: `min 40 / max 201 / avg 106.04`
- Duration(초): `min 124 / max 240 / avg 205.48`
- BPM 구간:
  - `fast (>=130)`: 39
  - `mid (90~129)`: 99
  - `slow (<90)`: 62

### 2-4. Keyscale
- Major 101 / Minor 99 (거의 1:1)
- 상위 key 예시:
  - E minor(20), G major(17), D minor(14), F minor(13), D major(12), C major(12), A major(12)

---

## 3) 장르/스타일 전체 분류 목록

아래는 text2music caption에 실제 등장하는 장르/스타일을 계층으로 정리한 목록.

### 3-1. Pop 계열
- Pop
- C-pop
- J-pop
- K-pop
- Mandopop
- Idol Pop / School Idol
- City Pop
- Synth-pop
- Electro-pop
- Pop-rock
- Pop Ballad
- Pop-rap

### 3-2. Rock/Metal 계열
- Rock
- J-rock
- Indie Rock
- Post-rock
- Progressive Rock
- Punk Rock
- Visual Kei Rock
- Gothic Rock
- Blues Rock
- Metal
- Industrial Metal
- Rock Ballad / Power Ballad

### 3-3. Hip-hop / Trap / R&B / Soul 계열
- Hip-hop
- Trap
- Latin Trap
- Boom-bap Hip-hop
- Lo-fi Hip-hop
- R&B
- K-R&B
- Neo-soul
- Soul / Soul Ballad
- Gospel-influenced Pop/Soul

### 3-4. EDM / Electronic 계열
- EDM
- Electronic Dance Music
- Techno
- House / French House
- Tropical House
- Synthwave
- Hyperpop
- Chiptune
- Vocaloid-style Pop
- New Wave / Neue Deutsche Welle

### 3-5. Jazz / Funk / Blues / Lounge 계열
- Jazz
- Jazz Vocal / Lounge
- Bossa Nova
- Funk / Funk-pop
- Disco
- Blues

### 3-6. Folk / Traditional / World / Function 계열
- Folk
- Country-folk
- Singer-songwriter
- Enka
- Trot
- Chanson
- Schlager Pop
- Reggae / Reggae-pop
- Samba-pop
- Waltz
- Military March
- Chinese Opera Fusion
- New Age / Meditation
- Lullaby
- Spoken Word / Slam

### 3-7. Cinematic / Anime / OST 계열
- Anime Theme Song
- Anime Opening
- Anime Ending
- Anime Battle Theme
- Cinematic Orchestral
- Fantasy RPG Theme

---

## 4) 장르 매핑표 (빈도 + 대표 예제)

> count는 caption에 해당 장르 키워드가 명시된 건수 기준(중복 가능).

| 장르 | count | 대표 example |
|---|---:|---|
| Anime Theme Song | 3 | example_01, example_06, example_106 |
| Anime Opening | 1 | example_131 |
| Anime Ending | 1 | example_137 |
| Anime Battle Theme | 1 | example_141 |
| J-pop | 7 | example_06, example_09, example_132, example_139 |
| K-pop | 7 | example_11, example_156, example_162, example_164 |
| C-pop | 4 | example_102, example_25, example_48, example_96 |
| Mandopop | 1 | example_04 |
| City Pop | 2 | example_134, example_16 |
| Idol Pop / School Idol | 2 | example_114, example_144 |
| Hyperpop | 1 | example_09 |
| Chiptune | 8 | example_09, example_14, example_155, example_25 |
| Vocaloid-style Pop | 1 | example_155 |
| Pop-rock | 6 | example_01, example_05, example_06, example_12 |
| J-rock | 7 | example_05, example_106, example_131, example_24 |
| Indie Rock | 5 | example_104, example_161, example_40, example_46 |
| Post-rock | 2 | example_108, example_145 |
| Progressive Rock | 2 | example_126, example_85 |
| Punk Rock | 5 | example_121, example_149, example_184, example_39 |
| Visual Kei Rock | 1 | example_135 |
| Gothic Rock | 1 | example_188 |
| Blues Rock | 2 | example_129, example_56 |
| Metal | 6 | example_113, example_176, example_34, example_36 |
| Industrial Metal | 2 | example_176, example_36 |
| Rock Ballad / Power Ballad | 5 | example_113, example_167, example_183, example_79 |
| Hip-hop | 17 | example_100, example_125, example_138, example_148 |
| Trap | 16 | example_02, example_03, example_118, example_158 |
| Latin Trap | 1 | example_02 |
| Boom-bap Hip-hop | 6 | example_13, example_169, example_181, example_20 |
| Lo-fi Hip-hop | 6 | example_125, example_148, example_169, example_17 |
| R&B | 8 | example_10, example_154, example_159, example_171 |
| K-R&B | 1 | example_159 |
| Neo-soul | 2 | example_159, example_76 |
| Soul / Soul Ballad | 3 | example_123, example_159, example_76 |
| Gospel-influenced Pop/Soul | 3 | example_107, example_123, example_57 |
| EDM | 5 | example_11, example_151, example_156, example_166 |
| Electronic Dance Music | 1 | example_109 |
| Techno | 1 | example_179 |
| House / French House | 2 | example_174, example_190 |
| Tropical House | 1 | example_174 |
| Synthwave | 2 | example_116, example_67 |
| Synth-pop | 3 | example_16, example_185, example_22 |
| Electro-pop | 2 | example_07, example_82 |
| New Wave / NDW | 1 | example_180 |
| Jazz | 5 | example_105, example_171, example_193, example_42 |
| Jazz Vocal / Lounge | 3 | example_105, example_140, example_64 |
| Bossa Nova | 2 | example_120, example_140 |
| Funk / Funk-pop | 4 | example_128, example_186, example_41, example_58 |
| Disco | 6 | example_146, example_164, example_186, example_190 |
| Blues | 3 | example_129, example_37, example_56 |
| Folk | 10 | example_101, example_115, example_142, example_175 |
| Country-folk | 2 | example_115, example_31 |
| Singer-songwriter | 2 | example_187, example_84 |
| Enka | 1 | example_136 |
| Trot | 1 | example_160 |
| Chanson | 1 | example_189 |
| Schlager Pop | 1 | example_177 |
| Reggae / Reggae-pop | 6 | example_112, example_198, example_26, example_33 |
| Samba-pop | 1 | example_08 |
| Waltz | 3 | example_117, example_182, example_196 |
| Military March | 1 | example_124 |
| Chinese Opera Fusion | 1 | example_110 |
| Cinematic Orchestral | 3 | example_130, example_163, example_71 |
| Fantasy RPG Theme | 1 | example_153 |
| New Age / Meditation | 1 | example_122 |
| Lullaby | 1 | example_150 |
| Spoken Word / Slam | 1 | example_199 |

---

## 5) caption 문장 구조 분석 (악기/음색/이펙트 중심)

caption은 대체로 아래 구조를 반복.

```mermaid
flowchart LR
A[장르+무드 선언] --> B[그루브/리듬 엔진]
B --> C[핵심 악기 편성]
C --> D[보컬 캐릭터]
D --> E[편곡 전개 빌드/브레이크/드롭]
E --> F[마무리 지시 페이드/테이프스탑/어브럽트]
```

### 5-1. 악기/편성 지시 빈도 (caption 기준)
| 항목 | caption 포함 수 | 대표 예시 |
|---|---:|---|
| Synthesizer | 91 | example_01, example_02, example_03, example_04 |
| Bass(808/sub 포함) | 91 | example_01, example_02, example_03, example_04 |
| Drums/Drum Machine | 86 | example_01, example_02, example_03, example_04 |
| Electric Guitar | 48 | example_01, example_04, example_05, example_06 |
| Piano/Keys | 48 | example_06, example_101, example_103, example_105 |
| Choir/Group Vocals | 37 | example_05, example_10, example_105, example_107 |
| Strings | 30 | example_103, example_106, example_111, example_117 |
| Acoustic Guitar | 23 | example_08, example_101, example_111, example_115 |
| Brass | 22 | example_01, example_08, example_123, example_124 |
| Percussion(world/aux) | 20 | example_110, example_112, example_119, example_120 |
| Woodwinds/Traditional Winds | 8 | example_101, example_119, example_122, example_136 |

### 5-2. 보컬 캐릭터 지시
| 항목 | caption 포함 수 | 해석 |
|---|---:|---|
| Male Vocal Lead | 155 | 남성 단독 리드 중심 설계 |
| Female Vocal Lead | 66 | 여성 리드 + 고음/감성 강조 |
| Duet/Mixed Lead | 6 | 남녀 교차/하모니 서사 |
| Rap Delivery | 22 | verse 랩 + chorus 멜로디 훅 패턴 |
| Falsetto/High Notes | 34 | 코러스 고조 포인트 |
| Breathy/Whispery | 10 | 친밀/몽환/야간 무드 |
| Theatrical/Operatic | 7 | 뮤지컬/고딕/서사 극대화 |
| Vocal Processing | 15 | auto-tune/vocoder/chops로 디지털 캐릭터 부여 |
| Ad-libs/Hype Shouts | 21 | 훅 반복/현장감 강화 |

### 5-3. 음색/프로덕션 이펙트 지시
| 항목 | caption 포함 수 | 특징 |
|---|---:|---|
| Reverb/Ambience | 50 | 공간감, 몽환감, 여운 |
| Delay/Echo | 9 | 랩 애드립 tail/보컬 잔향 |
| Sidechain/Pump | 3 | EDM 드롭 펌핑감 |
| Filtered FX | 10 | 브레이크 전후 대비, 전환 강조 |
| Vinyl/Lo-fi Texture | 25 | 레트로, 빈티지, 늦은 밤 질감 |
| Build-up/Drop/Breakdown | 53 | 에너지 곡선 제어 핵심 장치 |
| Crescendo/Dynamic Build | 9 | 발라드/오케스트라 클라이맥스 |

### 5-4. 무드/정서 지시
| 무드 | caption 포함 수 | 대표 용도 |
|---|---:|---|
| High-energy / Explosive | 44 | 오프닝/댄스/록 앤썸 |
| Uplifting / Celebratory | 18 | 졸업/희망/축제 |
| Melancholic / Bittersweet | 37 | 이별/회상/감성 발라드 |
| Dark / Aggressive | 36 | 트랩/메탈/반항 서사 |
| Romantic / Intimate | 30 | 러브송/듀엣/R&B |
| Chill / Relaxed | 42 | lo-fi/레게/카페/야간 청취 |

---

## 6) 가사 `[]` 지문 분석

### 6-1. 전체 통계
- 총 태그 수(언어태그 제외): `1714`
- 고유 태그 수: `154`

### 6-2. 파트(core) 사용 빈도
| core 태그 | count |
|---|---:|
| Chorus | 393 |
| Verse 1 | 201 |
| Intro | 200 |
| Verse 2 | 197 |
| Outro | 193 |
| Bridge | 126 |
| Pre-Chorus | 109 |
| Verse 3 | 77 |
| Instrumental Break | 36 |
| Guitar Solo | 16 |
| Drop | 14 |
| Final Chorus | 14 |
| Hook | 10 |
| Build-up | 9 |
| Breakdown | 8 |

### 6-3. 상세 지시어(detail) 상위
`[파트 - 상세지시]` 형태에서 detail 집계:

| detail | count |
|---|---:|
| Guitar Riff | 8 |
| Duet | 7 |
| Chiptune Synth Melody | 6 |
| Vocal Chop Melody | 4 |
| Female | 4 |
| Male | 4 |
| Layered Vocals | 3 |
| Electric Guitar Melody | 3 |
| Instrumental Drop | 3 |
| Saxophone Solo | 3 |
| Synth Bass Riff | 3 |
| Both | 3 |
| Synth Brass Melody | 2 |
| Instrumental Fade Out | 2 |
| Male Vocal | 2 |
| Guitar Melody | 2 |
| Acoustic Guitar | 2 |
| Brass Section | 2 |
| Arpeggiated Electric Guitar | 2 |

### 6-4. `[]` 지문 타입 분류

#### A. 구조 파트 지시
- Intro / Verse / Pre-Chorus / Chorus / Bridge / Outro
- 기능: 곡의 기본 서사 구조 고정

#### B. 악기/사운드 지정 지시
- 예: `[Intro - Synth Brass Fanfare]`, `[Instrumental Break - Guitar Melody]`
- 기능: 파트별 중심 음색 앵커 설정

#### C. 보컬 역할 지시
- 예: `[Chorus - Duet]`, `[Verse 2 - Male Rap]`, `[Chorus - Layered Vocals]`
- 기능: 화자 전환/밀도 증가/후렴 강조

#### D. 에너지 전개 지시
- Drop / Build-up / Breakdown / Instrumental Drop
- 기능: 클럽형/EDM형 에너지 곡선 제어

#### E. 엔딩 처리 지시
- Song fades out / Song ends abruptly / Final chord fades out
- 기능: 여운형 vs 충격형 종료 선택

### 6-5. 장르별로 자주 붙는 지문 패턴
- Rock/J-rock/Pop-rock:
  - `Intro - Guitar Riff`
  - `Instrumental Break - Guitar Melody`
  - `Guitar Solo`
- EDM/Hyperpop/Chiptune:
  - `Drop`, `Build-up`, `Instrumental Drop`
  - `Synth ...`, `Vocal Chop ...`
- Ballad/R&B/Soul:
  - `Bridge`, `Final Chorus`, `Layered Vocals`
  - `Outro - ... Fade Out`
- Jazz/City Pop/Lounge:
  - `Instrumental Break - Saxophone Solo`
  - `Piano ...`, `Brass Section`
- Folk/Acoustic:
  - `Acoustic Guitar`, `Harmonica ...`
  - 절제된 Instrumental Break + Fade Out

---

## 7) 요청하신 포인트 직접 답변

### Q1. "장르만 말고 caption 설명 방식 분류"
caption은 단순 장르명이 아니라 다음 6축을 동시에 지시:
1. 장르/스타일
2. 리듬 엔진(beat, groove, drum type)
3. 편성(악기군/음색)
4. 보컬 캐릭터(성별, 랩/가창, 톤, 기법)
5. 프로덕션 이펙트(reverb, filter, chops, sidechain 등)
6. 곡 구조(빌드, 브레이크, 드롭, 브리지, 엔딩)

### Q2. "[] 지문에서 장르별 지시사항"
- 지문은 "파트 구조" + "사운드/보컬 상세"를 결합해 모델에 시간축 편곡 지시를 줌
- 예: `[Intro - Synth Brass Fanfare]`
  - 구조: Intro 시작 구간 명시
  - 음색: Synth + Brass 톤
  - 역할: Fanfare(도입부 선언적 에너지)
  - 장르 친화도: Anime theme / Pop-rock / Cinematic 계열과 결합이 잦음

---

## 8) 실전 프롬프트 설계 체크리스트
- 장르 1~2개 + 하위 스타일 1개까지만 핵심축 고정
- 리듬 엔진을 명확히 (`four-on-the-floor`, `trap hi-hats`, `waltz 3/4`)
- 핵심 악기 3~5개 지정(리듬/화성/리드 분리)
- 보컬 지시(성별/톤/기법)와 후렴 확장 방식(ad-lib, layered, duet) 명시
- 전개 지시(`Build-up -> Drop`, `Bridge -> Final Chorus`)를 시간축으로 배치
- 엔딩 타입(Fade out / Abrupt end / Final chord) 명시

---

## 9) 결론
- 이 데이터셋은 **장르명 단일 입력형**이 아니라 **편곡 지시형 메타프롬프트** 구조임
- 성능이 잘 나오는 프롬프트는 장르보다도 **리듬 엔진 + 음색 앵커 + 보컬 지시 + 구조 전개**를 함께 지정
- `[]` 가사 지문은 단순 섹션 라벨이 아니라, 파트별 사운드 연출을 고정하는 **미니 어레인지 스코어** 역할

---

## 10) 추가 업데이트 (요청 반영)

### 10-1. Korean lo-fi 지시어 위치 (최우선 답변)
- 직접 표기:
  - `text2music/example_169.json`
  - caption: `A chill Korean lo-fi hip-hop track ...`
- 유사 표기(lo-fi aesthetic):
  - `text2music/example_161.json`
  - caption: `... nostalgic, lo-fi aesthetic reminiscent of Korean indie bands.`

### 10-2. 장르별 BPM / Key / 박자 범위 및 평균
> Key는 수치 평균보다 음악적 의미가 큰 범주형 값이므로, `모드 비율(Major/Minor)` + `상위 Keyscale`로 제시.

| Genre | N | BPM min~max (avg) | Timesignature | Key Mode | Top Keyscale |
|---|---:|---:|---|---|---|
| Korean Lo-fi Hip-hop | 1 | 78~78 (78.00) | 4:1 | Major:1 | Db major(1) |
| Lo-fi Hip-hop | 6 | 75~100 (84.33) | 4:6 | Major:5, Minor:1 | Db major(2), Ab major(1), B♭ major(1) |
| Hip-hop | 17 | 75~200 (106.71) | 4:17 | Minor:11, Major:6 | D minor(3), Db major(2), E minor(2) |
| Trap | 16 | 82~200 (114.69) | 4:16 | Minor:14, Major:2 | G minor(4), E minor(3), F minor(3) |
| R&B | 8 | 68~104 (85.50) | 4:8 | Major:6, Minor:2 | Eb major(2), A major(1), Ab major(1) |
| K-pop | 7 | 40~125 (101.43) | 4:7 | Major:4, Minor:3 | Ab major(1), B major(1), D major(1) |
| J-pop | 7 | 76~128 (103.14) | 4:5, 2:2 | Major:4, Minor:3 | F# major(2), C major(1), E♭ minor(1) |
| C-pop | 4 | 72~200 (125.00) | 4:3, 2:1 | Major:3, Minor:1 | Bb major(1), D minor(1), E♭ major(1) |
| Pop-rock | 6 | 100~100 (100.00) | 4:5, 2:1 | Major:3, Minor:3 | A major(1), B minor(1), C major(1) |
| J-rock | 7 | 40~200 (126.57) | 4:4, 2:3 | Minor:6, Major:1 | E minor(2), B minor(1), B♭ minor(1) |
| Indie Rock | 5 | 88~118 (100.20) | 4:5 | Major:4, Minor:1 | A major(2), D major(1), D minor(1) |
| Punk Rock | 5 | 100~185 (161.40) | 4:4, 2:1 | Major:4, Minor:1 | A major(2), E major(2), E minor(1) |
| Metal | 6 | 75~140 (113.33) | 4:6 | Minor:6 | D minor(2), E minor(2), B♭ minor(1) |
| EDM | 5 | 40~150 (114.20) | 4:5 | Minor:5 | A minor(1), E♭ minor(1), F minor(1) |
| Synthwave | 2 | 118~118 (118.00) | 4:2 | Minor:2 | A minor(1), F# minor(1) |
| Jazz | 5 | 68~100 (88.00) | 4:4, 2:1 | Major:4, Minor:1 | Ab major(1), Bb major(1), D minor(1) |
| Funk | 4 | 100~115 (107.75) | 4:4 | Minor:3, Major:1 | E minor(2), D minor(1), Bb major(1) |
| Disco | 6 | 115~126 (119.67) | 4:6 | Major:5, Minor:1 | Bb major(2), Ab major(1), D major(1) |
| Folk | 10 | 68~200 (105.50) | 4:6, 3:3, 2:1 | Major:7, Minor:3 | A minor(2), C major(2), D major(2) |
| Reggae | 6 | 82~100 (94.00) | 4:6 | Major:4, Minor:2 | G major(3), A major(1), A minor(1) |
| Bossa Nova | 2 | 92~105 (98.50) | 4:2 | Major:2 | Eb major(1), F major(1) |
| Waltz | 3 | 88~95 (90.33) | 3:3 | Major:3 | D major(2), Eb major(1) |
| Anime Theme | 5 | 100~178 (134.20) | 4:4, 2:1 | Minor:3, Major:2 | A major(1), B minor(1), D minor(1) |
| Cinematic Orchestral | 3 | 65~88 (79.33) | 4:3 | Major:3 | D major(2), Bb major(1) |

### 10-3. 장르별 자주 붙는 가사 지문 패턴 (상세)

| Genre | Core Top Pattern | Detail Top Pattern | 대표 예제 |
|---|---|---|---|
| Korean Lo-fi Hip-hop | Hook, Intro, Verse1/2, Outro | Hook 반복 | example_169 |
| Lo-fi Hip-hop | Chorus, Intro, Outro, Verse1/2 | `Chorus: Duet`, `Instrumental Break: Saxophone Solo` | example_125, example_148, example_169, example_21 |
| Trap | Chorus, Intro, Verse1/2, Hook | `Instrumental Drop`, Bridge 다수 | example_02, example_03, example_118, example_158 |
| K-pop | Chorus, Pre-Chorus, Bridge | Build-up 이후 Chorus 집중 | example_11, example_156, example_162 |
| J-pop | Chorus, Pre-Chorus, Intro/Outro | `Instrumental Break` 비중 큼 | example_06, example_09, example_132 |
| Pop-rock | Chorus, Pre-Chorus, Bridge | `Guitar Solo` / Guitar 기반 지시 | example_01, example_05, example_12 |
| J-rock | Chorus, Pre-Chorus, Verse1/2 | `Guitar Solo` + Bridge 강세 | example_05, example_131, example_34 |
| Punk Rock | Chorus, Verse1/2, Intro/Outro | 구조 단순, 고속 반복 | example_121, example_149, example_184 |
| Metal | Chorus, Verse1/2, Pre-Chorus | `Breakdown` 출현 | example_113, example_176, example_75 |
| EDM | Build-up, Drop, Intro/Outro | `Build-up -> Drop` 고정형 | example_11, example_151, example_166 |
| Folk | Chorus, Verse1/2/3, Intro/Outro | Verse 확장형(스토리텔링) | example_101, example_142, example_175 |
| Waltz | Chorus + Verse1/2/3 균형 | 3/4 기반 반복 | example_117, example_182, example_196 |
| Anime Theme | Chorus, Pre-Chorus, Verse1/2 | Final Chorus/Bridge 강조 | example_01, example_131, example_141 |
| Cinematic Orchestral | Chorus, Bridge, Verse1/2 | Final Chorus/클라이맥스형 | example_130, example_163, example_71 |

### 10-4. 5-2 / 5-3 / 5-4 사용빈도 + 대표 예제 매핑 강화

#### 5-2 보컬 캐릭터 지시
| 항목 | 사용빈도 | 대표 예제 |
|---|---:|---|
| Male Vocal Lead | 155 | example_01, example_02, example_03, example_04, example_05 |
| Female Vocal Lead | 66 | example_09, example_102, example_103, example_105, example_106 |
| Duet/Mixed Lead | 6 | example_103, example_139, example_200, example_21, example_66 |
| Rap Delivery | 22 | example_03, example_07, example_100, example_118, example_13 |
| Falsetto/High Notes | 34 | example_01, example_04, example_06, example_10, example_103 |
| Breathy/Whispery | 10 | example_10, example_120, example_157, example_174, example_18 |
| Theatrical/Operatic | 7 | example_01, example_135, example_173, example_188, example_196 |
| Vocal Processing | 15 | example_02, example_03, example_09, example_11, example_118 |
| Ad-libs/Hype Shouts | 21 | example_02, example_03, example_04, example_05, example_06 |

#### 5-3 음색/프로덕션 이펙트 지시
| 항목 | 사용빈도 | 대표 예제 |
|---|---:|---|
| Reverb/Ambience | 50 | example_02, example_03, example_05, example_07, example_104 |
| Delay/Echo | 9 | example_02, example_05, example_108, example_13, example_18 |
| Sidechain/Pump | 3 | example_109, example_174, example_82 |
| Filtered FX | 10 | example_03, example_09, example_11, example_13, example_14 |
| Vinyl/Lo-fi Texture | 25 | example_104, example_116, example_125, example_13, example_134 |
| Build-up/Drop/Breakdown | 53 | example_01, example_02, example_04, example_07, example_08 |
| Crescendo/Dynamic Build | 9 | example_04, example_07, example_108, example_135, example_145 |

#### 5-4 무드/정서 지시
| 항목 | 사용빈도 | 대표 예제 |
|---|---:|---|
| High-energy / Explosive | 44 | example_01, example_05, example_07, example_09, example_11 |
| Uplifting / Celebratory | 18 | example_01, example_06, example_08, example_102, example_107 |
| Melancholic / Bittersweet | 37 | example_02, example_104, example_108, example_111, example_116 |
| Dark / Aggressive | 36 | example_02, example_03, example_09, example_118, example_121 |
| Romantic / Intimate | 30 | example_10, example_101, example_103, example_117, example_120 |
| Chill / Relaxed | 42 | example_06, example_107, example_111, example_112, example_113 |

### 10-5. 6번(가사 파트 사용 빈도) 장르별 정리

| Genre | Top Part Frequency |
|---|---|
| Hip-hop | Chorus(26), Intro/Outro(17), Verse1/2(17), Hook(8) |
| Trap | Chorus(30), Intro/Outro/Verse1/2(16), Hook(6) |
| R&B | Chorus(16), Intro/Outro/Pre-Chorus(8), Verse1/2(7) |
| K-pop | Chorus(14), Pre-Chorus(12), Bridge(7), Intro/Outro(7) |
| J-pop | Chorus(16), Pre-Chorus(8), Intro/Outro/Verse2(7) |
| Pop-rock | Chorus(16), Pre-Chorus(8), Bridge(6), Verse1/2(6) |
| J-rock | Chorus(17), Pre-Chorus(9), Verse1/2/Bridge(7) |
| Punk Rock | Chorus(11), Verse1/2(5), Intro/Outro(5) |
| Metal | Chorus(14), Verse1/2(6), Pre-Chorus(5) |
| EDM | Build-up(6), Drop(6), Intro/Outro(5), Bridge(4) |
| Folk | Chorus(21), Verse1/2/3(10/10/9), Intro(10), Outro(9) |
| Waltz | Chorus(7), Intro/Outro/Verse1/2/3(3씩) |
| Anime Theme | Chorus(11), Pre-Chorus(6), Intro/Outro/Verse1/2(5) |
| Cinematic Orchestral | Chorus(6), Bridge(3), Intro/Outro/Verse1/2(3) |

