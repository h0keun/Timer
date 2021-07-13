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
#### Kotlin.class - MainActivity.kt
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
  * private val soundPool = SoundPool.Builder().build() 
    // 사운드풀을 전역으로 선언하고 빌드하기. 이는 onCreate()에서 initSound() 에서 실행
  ```    
+ 사운드 재생시키기위한 사전작업?
  ```KOTLIN
  *onCreate() 에서 initSounds() 를 호출
  
  private fun initSounds() {
      tickingSoundId = soundPool.load(this, R.raw.timer_ticking, 1)
      bellSoundId = soundPool.load(this, R.raw.timer_bell, 1)
  }
  
  // tickingSoundId, bellSoundId 는 Int? 값으로 초기값 null인 전역변수로 선언한 상태
  ```
+ seekBar와 분,초 텍스트뷰 - 바인딩 시키기
  : 분, 초 를 나타내는 텍스트뷰와 SeekBar를 바인딩하여 SeekBar의 진행상황에 맞추어 분, 초가 변경되어 표시되도록 해야한다.
  ```KOTLIN
  * onCreate()에서 bindViews() 를 호출

  private fun bindViews() {
      seekBar.setOnSeekBarChangeListener(
          object : SeekBar.OnSeekBarChangeListener {
              override fun onProgressChanged(seekBar: SeekBar?, progress: Int, fromUser: Boolean) {
                  if (fromUser) {
                      updateRemainTime(progress * 60 * 1000L)
                  }
              }

              override fun onStartTrackingTouch(seekBar: SeekBar?) {
                  stopCountDown()
              }

              override fun onStopTrackingTouch(seekBar: SeekBar?) {
                  seekBar ?: return

                  if (seekBar.progress == 0) {
                      stopCountDown()
                  } else {
                      startCountDown()
                  }
              }
          }
      )
  }
  
  * OnSeekBarChangeListener 는 seekbar 상태 변경시 자동호출되는 콜백 이벤트이며, 아래와 같은 메서드를 상속받는다.
    onProgressChanged : 드래그 중 발생(프로그래스가 바뀌고있는 상황)
    onStartTrackingTouch : 최초 탭하여 드래그 시작시 발생(터치가 이루어지고있는상황)
    onStopTrackingTouch : 드래그 멈추면 발생(터치를 멈춘상황 == 바에서 손을 떼는 순간)
    
  * 코드를 보면 SeekBar의 이벤트 리스너로 object로 선언하여 만들어준 객체를 지정하였는데,
    관련된 지식이 부족하여 타인의 말을 빌려보자면,
    object로 선언하게 되면 해당 이벤트 리스너가 지정해둔 인터페이스를 
    우리가 알맞게 재정의 해줌 으로써 이벤트 리스너를 설정하게 된다고 한다.
    각각 onProgressChanger, onStartTrackingTouch, onStopTrackingTouch 인터페이스 함수를 재정의 해주어야 하며
    이는 각각 위에 언급한 동작에 맞추어 진행된다.
  ```
+ onProgressChanged : 사용자 터치에의해 시크바가 변경될 때
  ```KOTLIN
  * 유저가 thumb를 움직인 경우 해당하는 progress를 남은 시간으로 재설정해준다.
  * updateRemainTime(progress * 60 * 1000L) 실행

  private fun updateRemainTime(remainMillis: Long) {
      val remainSeconds = remainMillis / 1000

      remainMinutesTextView.text = "%02d'".format(remainSeconds / 60)
      remainSecondsTextView.text = "%02d".format(remainSeconds % 60)
  }
  ```
+ onStartTrackingTouch : 사용자가 바에 손을 가져다 대는 순간 실행
  ```KOTLIN
  * 시크바 조정 시 새로운 타이머를 동작시키기위해 카운트 다운을 멈추고,
    onStopTrackingTouch 에서 터치가 멈춘 경우 새로운 타이머를 시작되도록 한다.
  * stopCountDown()

  private fun stopCountDown() {
      currentCountDownTimer?.cancel()
      currentCountDownTimer = null
      soundPool.autoPause()
  } 
  ```
+ onStopTrackingTouch : 사용자가 바에서 손을 떼는 순간 실행
  ```KOTLIN
  // 이 때 seekbar가 0이면 stopCountDown()을, 그렇지 않으면 startCountDown()을 실행
  
  * stopCountDown()  
  private fun stopCountDown() {
      currentCountDownTimer?.cancel()
      currentCountDownTimer = null
      soundPool.autoPause()
  }  
  
  * startCountDown() 
  private fun startCountDown() {
      currentCountDownTimer = createCountDownTimer(seekBar.progress * 60 * 1000L)
      currentCountDownTimer?.start() 

      tickingSoundId?.let { soundId ->
          soundPool.play(soundId, 1F, 1F, 0, -1, 1F)
      }
  }
  
  // currentCounDownTimer 는 CountDownTimer? 값으로 초기값 null인 전역변수로 선언한 상태
  // 이때 soundPool은 디바이스 자체에 요청하는 것이기 때문에 화면 종료시에도 계속 재생될 수 있다.
  // 떄문에 생명주기에 따른 처리가 필요하다!
  
  * createCountDownTimer

  private fun createCountDownTimer(initialMillis: Long) =
          object : CountDownTimer(initialMillis, 1000L) {
              override fun onTick(millisUntilFinished: Long) {
                  updateRemainTime(millisUntilFinished)
                  updateSeekBar(millisUntilFinished)
              }

              override fun onFinish() {
                  completeCountDown()
              }
          }
          
  // onTick() 에서 타이머가 작동할 때 어떤 동작을 할지 설정(남은시간, 시크바를 밀리초에 맞게 설정)
  // onFinish() 에서 카운트 다운 완료 처리 함수를 호출(completeCountDown())
  
  * updateRemainTime() 과 updateSeekBar 에서는 남은 밀리초를 기준으로 텍스트뷰와 프로그래스바를 설정해줌

  private fun updateRemainTime(remainMillis: Long) {
      val remainSeconds = remainMillis / 1000

      remainMinutesTextView.text = "%02d'".format(remainSeconds / 60)
      remainSecondsTextView.text = "%02d".format(remainSeconds % 60)
  }
  
  private fun updateSeekBar(remainMillis: Long) {
      seekBar.progress = (remainMillis / 1000 / 60).toInt()
  }
  
  * completeCountDown()

  private fun completeCountDown() {
      updateRemainTime(0)
      updateSeekBar(0)

      soundPool.autoPause()
      bellSoundId?.let { soundId ->
          soundPool.play(soundId, 1F, 1F, 0, 0, 1F)
      }
  }
  
  // tick 사운드를 멈추고 bell사운드를 실행시킴
  // tick 사운드는 loop 파라미터가 -1로 계속 반복되며, bell 사운드는 loop 파라미터가 0으로 한번만 실행된다.
  ```
+ 생명주기에 따라 soundPool 설정
  ```KOTLIN
  onResume() -> soundPool.autoResume()  // 앱이 다시 시작
  onPause() -> soundPool.autoPause()    // 앱이 화면에 보이지 않음
  onDestroy() -> soundPool.release()    // 더이상 앱을 사용하지 않을 때 사운드풀을 메모리에서 해제
  
  * soundPool load, play
  
    load() 메소드 : 소리파일을 로드하여 그 아이디(soundId)를 반환  
    play() 메소드 : 소리를 재생  
    
    load()와 play()에 들어가는 파라미터에는 
    context, resId, priority, soundId, leftVolume, RightVolume, loop, rate 등 이있으며, 
    이를통해 재생할 raw 디렉터리의 mp4 파일 리소스를 지정하고 재생하며, 
    양쪽 볼륨을 지정하고, 우선순위(0이 가장 낮음), 
    반복(0이면 반복하지않고, -1이면 반복), 재생속도(1.0배속) 등을 설정할 수 있다. 
    이외에 다른 여러기능들은 공식문서 참조!
  ```     

💡 비교정리 필요한 내용들  
```KOTLIN
이전에 부스트코스에서 학습한 AsycTask 에서 쓰레드활용해서 progressbar를 구현했었음
Melon 클론코딩할때 seekbar 사용했었는데 음악재생에 맞추어 seekbar 이동하도록 구현했었음
본 프로젝트 타이버에서 seekbar 사용하는데 timer 함께

위에 언급한 세부분들에대해서 명확히 구분짓고 왜 해당방식으로 구현했으며, 무슨차이점이 있는지 등  
확실하게 알아볼 필요가 있을거 같다.
```
💡 Kotlin에서 object 로 선언하는 이유?? 
```KOTLIN
object로 선언하면 클래스 선언과 동시에 인스턴스(객체)가 생성된다고한다.
object 객체 역시 다른 class를 상속하거나 interface를 구현할수 있다.
🥕🥕🥕🥕🥕🥕🥕🥕🥕🥕 반드시 집고 넘어갈 필요가 있음!!
싱글톤 패턴, 팩토리 패턴 등에 유용하다고 하는데 companion object와 더불어서 하루 날잡고 공부해야겠다.
이부분은 추가적으로 검색해서 알아봐야할거 같다. 왜 클래스 선언과 동시에 객체를 생성해야하는지
등 정확히 객체와 클래스는 뭔지 등 뭔가 나사하나 빠져있는 기분
```
