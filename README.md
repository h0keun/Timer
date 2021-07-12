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
### [2021-07-12]

#### xml
+ themes.xml
  ```KOTLIN
  <item name="android:statusBarColor" tools:targetApi="l">@color/pomodoro_red</item>
  <item name="android:windowBackground">@color/pomodoro_red</item>
  
  * 상태바와 배경색을 임의의 동일한 색상으로 변경
  ```
+ activity_main.xml - ConstraintLayout
  ```KOTLIN
  * 위 스크린샷에 보이는 토마토 꼭지이미지는 vector 이미지를 ImageView에 지정해 준 것이며,
  
  * 00'00 은 분과 초를 각각 TextView로 표현한 것이다. 이때, 분과 초 텍스트뷰의 정렬을 constraintLayout 속성을 이용하여 
  top을 top에 맞춰주고 bottom을 bottom 에 맞춰주게 되면 그림과 같이 아래정렬로 맞춰지는것이 아니라 중앙정렬로 맞춰지게 된다.
  이를 해결하기위해 초 텍스트뷰에 아래와 같은 속성을 추가하여 분에 해당하는 텍스트뷰의 베이스 라인으로 정렬을 해주었다.
  app:layout_constraintBaseline_toBaselineOf="@id/remainMinutesTextView"  
  
  * 맨아래에 SeekBar은 따로 커스텀하여 틱마크와 Thumb 등을 지정해주었다.
  ```
+ activity_main.xml - SeekBar custom
  ```KOTLIN
  <SeekBar
     android:id="@+id/seekBar"
     android:layout_width="0dp"
     android:layout_height="wrap_content"
     android:layout_marginHorizontal="20dp"
     android:max="60"
     android:progressDrawable="@color/transparent"
     android:thumb="@drawable/ic_thumb"
     app:layout_constraintBottom_toBottomOf="parent"
     app:layout_constraintLeft_toLeftOf="parent"
     app:layout_constraintRight_toRightOf="parent"
     app:layout_constraintTop_toBottomOf="@id/remainMinutesTextView"
     app:tickMark="@drawable/drawable_tick_mark" />
  
  * max값 60을 줌으로써 seekbar가 60개의 칸으로 나누어짐 
    : 60분에 한칸은 1분을 나타내기 위함
  * progressDrawble은 seekbar의 선을 나타낸다. 
    : 투명하게 설정하여 seekBar를 보이지 않게 하고, tickMark를 지정해주어 60 tick이 보여진다.
    (tickMark는 max로 나누어진 60개의 칸을 보여주는데, seekbar에서 커서가 움직일 때 안착하는 곳? 이라고 생각하면 될듯)
  * thumb는 seekbar위를 움직이는 커서를 나타낸다. (Vector 이미지)
  ```
+ drawable_tick_mark.xml
  ```KOTLIN
  <?xml version="1.0" encoding="utf-8"?>
  <shape xmlns:android="http://schemas.android.com/apk/res/android"
      android:shape="rectangle">

      <solid android:color="@color/white"/>
      <size android:width="2dp" android:height="5dp"/>

  </shape>
  
  * seekBar에서 tickMark를 커스텀
  ```
#### Kotlin.class
+ mp4 파일 추가
  ```KOTLIN
  📂 res ⁅ 
      📂 raw ⁅
          ‣ timer_bell.mp4
          ‣ timer_ticking.mp4
          
  * res 폴더에 raw 폴더를 추가하여 
    타이머 진행소리인 tinking 사운드와 타이머가 완료되었을때 울리는 bell 사운드를 추가하였따.
  ```
+ 안드로이드에서 사운드를 재생 시킬 때 
  ```KOTLIN
  SoundPool 혹은 MediaPlayer 를 사용한다.
  soundPool의 경우에는 알림소리 등과 같은 짧은 사운드클립(연타)에 적합하고, 
  MediaPlayer는 노래, 배경소리와 같이 큰 사운드파일(비디오파일)을 재생할 때 적합하다.
  
  * 본프로젝트에서는 SoudPool을 사용함
  ```    
   
  넘어가기전에 이전에 진행했던 melon 클론 프로젝트 확인하기  
  거기서도 seekBar를 커스텀하여 사용했었는데 뭐랄까 구분지을 필요가 있다?? 느낌?  
  이건 raw에따로 저장한 소리를 재생하는거고 melon은 api를 따로 만들어서 재생하는건데  
  그때는 쓰레드이용했던거 같은데, 하이튼 여기랑 좀 다름  
  
  
  
  
  
  
   
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
    
💡 Kotlin에서 object 로 선언하는 이유?? 
```KOTLIN
object로 선언하면 클래스 선언과 동시에 객체가 생성된다고한다.
object 객체 역시 다른 class를 상속하거나 interface를 구현할수 있다.

이부분은 추가적으로 검색해서 알아봐야할거 같다. 왜 클래서 선언과 동시에 객체를 생성해야하는지
등 정확히 객체와 클래스는 뭔지 등 뭔가 나사하나 빠져있는 기분
```
