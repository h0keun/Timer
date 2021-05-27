```💡 FastCampus 강의 수강 및 정리```

### Timer - 뽀모도로 타이머
+ ConstraintLayout
+ SeekBar
+ CountDownTimer
+ SoundPool
+ Lifecycle
+ Vector graphics(Drawable) : 다중밀도에 하나의 파일로 대응가능, 다만 비용이 크기때문에 간단한 모양으로(200x200)사이즈
+ 추상화..

### 기능
+ Mp4 재생(째깍소리, 알람소리) : Mp3나 Mp4 등의 음악파일은 res/raw 폴더 생성후 이곳에 추가
+ SeekBar custom(tickMark, thumb, progressDrawable) 

<img src="https://user-images.githubusercontent.com/63087903/119834410-e3747280-bf3a-11eb-864e-d7e6e9ee92dd.jpg" width="200" height="430">

### [2021-05-11]
+ layout.xml
  - ConstraintLayout 속성중  
    ```app:layout_constraintBaseline_toBaselineOf="@id/remainMinutesTextView"``` 를 이용하면  
    기존에 const botbot 과 toptop으로 연결시켰을 때 뷰가 중앙에 위치하게 되는것과 다르게
    아랫줄 라인을 기준으로 붙여서 위치시키는게 가능함  
  - SeekBar custom
    ```KOTLIN
    android:max="60"
    android:progressDrawable="@color/transparent"
    android:thumb="@drawable/ic_thumb"
    app:tickMark="@drawable/drawable_tick_mark"
    ```
    max값 60을 줌으로써 seekbar가 60개의 칸으로 나누어짐
    progressDrawble은 seekbar의 선을 나타내고, thum는 seekbar위를 움직이는 커서를 나타낸다.
    tickMark는 max로 나누어진 60개의 칸을 보여줌. seekbar에서 커서를 움직일 때 안착하는 곳? 이라고 생각하면 될듯

+ Kotlin.kt
  - 안드로이드에서 사운드를 재생 시킬 때 1.SoundPool 2.MediaPlayer 를 사용하는데
    soundPool의 경우에는 알림소리 등과 같은 짧은 사운드클립(연타)에 적합하고, MediaPlayer는 노래, 배경소리와 같이 큰 사운드파일(비디오파일)을 재생할 때 적합하다.
   
    1.. Builder().build() 메소드로 SoundPool 객체를 생성  
    2.. load() 메소드로 소리파일을 로드하여 그 아이디를 반환  
    3.. play() 메소드로 소리를 재생  
    
    load()와 play()에 들어가는 파라미터에는 context, resId, priority, soundId, leftVolume, RightVolume, loop, rate 등 이있으며, 이를통해 재생할 raw 디렉터리 소리파일 리소스를 지정하고 재생하며, 양쪽 볼륨을 지정하고, 우선순위(0이 가장 낮음), 반복(0이면 반복하지않고, -1이면 반복), 재생속도(1.0배속) 등을 설정할 수 있다. 이외에 다른 여러기능들은 공식문서 참조!
    ```KOTLIN
    private val soundPool = SoundPool.Builder().build()
    ...
    private fun initSounds() {
        tickingSoundId = soundPool.load(this, R.raw.timer_ticking, 1)
        bellSoundId = soundPool.load(this, R.raw.timer_bell, 1)
    }
    ...
    tickingSoundId?.let { soundId ->
        soundPool.play(soundId, 1F, 1F, 0, -1, 1F)
    }
    bellSoundId?.let { soundId ->
        soundPool.play(soundId, 1F, 1F, 0, 0, 1F)
    }
    ```
    주의해야할 점은 사운드 재생을 생명주기에 맞춰주어야 원할한 재생이 가능하다.
    ```KOTLIN
    onResume() -> soundPool.autoResume()
    onPause() -> soundPool.autoPause()
    onDestroy() -> soundPool.release()
    ```
  - Custom SeekBar  
    기능적인 부분을 담당하는 seekBar.setOnSeekBarChangeListener, countdowntimer 등 은 공식문서를 참조하는 편이 좋고, 
    이외의 부분들은 사용자의 터치에 따라 발생하는 이벤트들에대한 처리이기 때문에 수학적인 로직이 주를 이룬다.
    때문에 코드를 보며 확인하는편이 좋을듯 함!
    
💡 Kotlin에서 object : 싱글턴패턴?? 익명객체??
