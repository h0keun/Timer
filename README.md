```๐ก FastCampus ๊ฐ์ ์๊ฐ ๋ฐ ์ ๋ฆฌ```

### Timer - ๋ฝ๋ชจ๋๋ก ํ์ด๋จธ
+ ConstraintLayout
+ SeekBar
+ CountDownTimer
+ SoundPool
+ Lifecycle
+ Vector graphics(Drawable) : ๋ค์ค๋ฐ๋์ ํ๋์ ํ์ผ๋ก ๋์๊ฐ๋ฅ, ๋ค๋ง ๋น์ฉ์ด ํฌ๊ธฐ๋๋ฌธ์ ๊ฐ๋จํ ๋ชจ์์ผ๋ก(200x200)์ฌ์ด์ฆ
+ ์ถ์ํ..

### ๊ธฐ๋ฅ
+ Mp4 ์ฌ์(์งธ๊น์๋ฆฌ, ์๋์๋ฆฌ) : Mp3๋ Mp4 ๋ฑ์ ์์ํ์ผ์ res/raw ํด๋ ์์ฑํ ์ด๊ณณ์ ์ถ๊ฐ
+ SeekBar custom(tickMark, thumb, progressDrawable) 

<img src="https://user-images.githubusercontent.com/63087903/119834410-e3747280-bf3a-11eb-864e-d7e6e9ee92dd.jpg" width="200" height="430">

### [2021-05-11]
### [2021-07-12]

#### xml
+ themes.xml
  ```KOTLIN
  <item name="android:statusBarColor" tools:targetApi="l">@color/pomodoro_red</item>
  <item name="android:windowBackground">@color/pomodoro_red</item>
  
  * ์ํ๋ฐ์ ๋ฐฐ๊ฒฝ์์ ์์์ ๋์ผํ ์์์ผ๋ก ๋ณ๊ฒฝ
  ```
+ activity_main.xml - ConstraintLayout
  ```KOTLIN
  * ์ ์คํฌ๋ฆฐ์ท์ ๋ณด์ด๋ ํ ๋งํ  ๊ผญ์ง์ด๋ฏธ์ง๋ vector ์ด๋ฏธ์ง๋ฅผ ImageView์ ์ง์ ํด ์ค ๊ฒ์ด๋ฉฐ,
  
  * 00'00 ์ ๋ถ๊ณผ ์ด๋ฅผ ๊ฐ๊ฐ TextView๋ก ํํํ ๊ฒ์ด๋ค. ์ด๋, ๋ถ๊ณผ ์ด ํ์คํธ๋ทฐ์ ์ ๋ ฌ์ constraintLayout ์์ฑ์ ์ด์ฉํ์ฌ 
  top์ top์ ๋ง์ถฐ์ฃผ๊ณ  bottom์ bottom ์ ๋ง์ถฐ์ฃผ๊ฒ ๋๋ฉด ๊ทธ๋ฆผ๊ณผ ๊ฐ์ด ์๋์ ๋ ฌ๋ก ๋ง์ถฐ์ง๋๊ฒ์ด ์๋๋ผ ์ค์์ ๋ ฌ๋ก ๋ง์ถฐ์ง๊ฒ ๋๋ค.
  ์ด๋ฅผ ํด๊ฒฐํ๊ธฐ์ํด ์ด ํ์คํธ๋ทฐ์ ์๋์ ๊ฐ์ ์์ฑ์ ์ถ๊ฐํ์ฌ ๋ถ์ ํด๋นํ๋ ํ์คํธ๋ทฐ์ ๋ฒ ์ด์ค ๋ผ์ธ์ผ๋ก ์ ๋ ฌ์ ํด์ฃผ์๋ค.
  app:layout_constraintBaseline_toBaselineOf="@id/remainMinutesTextView"  
  
  * ๋งจ์๋์ SeekBar์ ๋ฐ๋ก ์ปค์คํํ์ฌ ํฑ๋งํฌ์ Thumb ๋ฑ์ ์ง์ ํด์ฃผ์๋ค.
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
  
  * max๊ฐ 60์ ์ค์ผ๋ก์จ seekbar๊ฐ 60๊ฐ์ ์นธ์ผ๋ก ๋๋์ด์ง 
    : 60๋ถ์ ํ์นธ์ 1๋ถ์ ๋ํ๋ด๊ธฐ ์ํจ
  * progressDrawble์ seekbar์ ์ ์ ๋ํ๋ธ๋ค. 
    : ํฌ๋ชํ๊ฒ ์ค์ ํ์ฌ seekBar๋ฅผ ๋ณด์ด์ง ์๊ฒ ํ๊ณ , tickMark๋ฅผ ์ง์ ํด์ฃผ์ด 60 tick์ด ๋ณด์ฌ์ง๋ค.
    (tickMark๋ max๋ก ๋๋์ด์ง 60๊ฐ์ ์นธ์ ๋ณด์ฌ์ฃผ๋๋ฐ, seekbar์์ ์ปค์๊ฐ ์์ง์ผ ๋ ์์ฐฉํ๋ ๊ณณ? ์ด๋ผ๊ณ  ์๊ฐํ๋ฉด ๋ ๋ฏ)
  * thumb๋ seekbar์๋ฅผ ์์ง์ด๋ ์ปค์๋ฅผ ๋ํ๋ธ๋ค. (Vector ์ด๋ฏธ์ง)
  ```
+ drawable_tick_mark.xml
  ```KOTLIN
  <?xml version="1.0" encoding="utf-8"?>
  <shape xmlns:android="http://schemas.android.com/apk/res/android"
      android:shape="rectangle">

      <solid android:color="@color/white"/>
      <size android:width="2dp" android:height="5dp"/>

  </shape>
  
  * seekBar์์ tickMark๋ฅผ ์ปค์คํ
  ```
#### Kotlin.class - MainActivity.kt
+ mp4 ํ์ผ ์ถ๊ฐ
  ```KOTLIN
  ๐ res โ 
      ๐ raw โ
          โฃ timer_bell.mp4
          โฃ timer_ticking.mp4
          
  * res ํด๋์ raw ํด๋๋ฅผ ์ถ๊ฐํ์ฌ 
    ํ์ด๋จธ ์งํ์๋ฆฌ์ธ tinking ์ฌ์ด๋์ ํ์ด๋จธ๊ฐ ์๋ฃ๋์์๋ ์ธ๋ฆฌ๋ bell ์ฌ์ด๋๋ฅผ ์ถ๊ฐํ์๋ฐ.
  ```
+ ์๋๋ก์ด๋์์ ์ฌ์ด๋๋ฅผ ์ฌ์ ์ํฌ ๋ 
  ```KOTLIN
  SoundPool ํน์ MediaPlayer ๋ฅผ ์ฌ์ฉํ๋ค.
  soundPool์ ๊ฒฝ์ฐ์๋ ์๋ฆผ์๋ฆฌ ๋ฑ๊ณผ ๊ฐ์ ์งง์ ์ฌ์ด๋ํด๋ฆฝ(์ฐํ)์ ์ ํฉํ๊ณ , 
  MediaPlayer๋ ๋ธ๋, ๋ฐฐ๊ฒฝ์๋ฆฌ์ ๊ฐ์ด ํฐ ์ฌ์ด๋ํ์ผ(๋น๋์คํ์ผ)์ ์ฌ์ํ  ๋ ์ ํฉํ๋ค.
  
  * ๋ณธํ๋ก์ ํธ์์๋ SoudPool์ ์ฌ์ฉํจ
  * private val soundPool = SoundPool.Builder().build() 
    // ์ฌ์ด๋ํ์ ์ ์ญ์ผ๋ก ์ ์ธํ๊ณ  ๋น๋ํ๊ธฐ. ์ด๋ onCreate()์์ initSound() ์์ ์คํ
  ```    
+ ์ฌ์ด๋ ์ฌ์์ํค๊ธฐ์ํ ์ฌ์ ์์?
  ```KOTLIN
  *onCreate() ์์ initSounds() ๋ฅผ ํธ์ถ
  
  private fun initSounds() {
      tickingSoundId = soundPool.load(this, R.raw.timer_ticking, 1)
      bellSoundId = soundPool.load(this, R.raw.timer_bell, 1)
  }
  
  // tickingSoundId, bellSoundId ๋ Int? ๊ฐ์ผ๋ก ์ด๊ธฐ๊ฐ null์ธ ์ ์ญ๋ณ์๋ก ์ ์ธํ ์ํ
  ```
+ seekBar์ ๋ถ,์ด ํ์คํธ๋ทฐ - ๋ฐ์ธ๋ฉ ์ํค๊ธฐ
  : ๋ถ, ์ด ๋ฅผ ๋ํ๋ด๋ ํ์คํธ๋ทฐ์ SeekBar๋ฅผ ๋ฐ์ธ๋ฉํ์ฌ SeekBar์ ์งํ์ํฉ์ ๋ง์ถ์ด ๋ถ, ์ด๊ฐ ๋ณ๊ฒฝ๋์ด ํ์๋๋๋ก ํด์ผํ๋ค.
  ```KOTLIN
  * onCreate()์์ bindViews() ๋ฅผ ํธ์ถ

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
  
  * OnSeekBarChangeListener ๋ seekbar ์ํ ๋ณ๊ฒฝ์ ์๋ํธ์ถ๋๋ ์ฝ๋ฐฑ ์ด๋ฒคํธ์ด๋ฉฐ, ์๋์ ๊ฐ์ ๋ฉ์๋๋ฅผ ์์๋ฐ๋๋ค.
    onProgressChanged : ๋๋๊ทธ ์ค ๋ฐ์(ํ๋ก๊ทธ๋์ค๊ฐ ๋ฐ๋๊ณ ์๋ ์ํฉ)
    onStartTrackingTouch : ์ต์ด ํญํ์ฌ ๋๋๊ทธ ์์์ ๋ฐ์(ํฐ์น๊ฐ ์ด๋ฃจ์ด์ง๊ณ ์๋์ํฉ)
    onStopTrackingTouch : ๋๋๊ทธ ๋ฉ์ถ๋ฉด ๋ฐ์(ํฐ์น๋ฅผ ๋ฉ์ถ์ํฉ == ๋ฐ์์ ์์ ๋ผ๋ ์๊ฐ)
    
  * ์ฝ๋๋ฅผ ๋ณด๋ฉด SeekBar์ ์ด๋ฒคํธ ๋ฆฌ์ค๋๋ก object๋ก ์ ์ธํ์ฌ ๋ง๋ค์ด์ค ๊ฐ์ฒด๋ฅผ ์ง์ ํ์๋๋ฐ,
    ๊ด๋ จ๋ ์ง์์ด ๋ถ์กฑํ์ฌ ํ์ธ์ ๋ง์ ๋น๋ ค๋ณด์๋ฉด,
    object๋ก ์ ์ธํ๊ฒ ๋๋ฉด ํด๋น ์ด๋ฒคํธ ๋ฆฌ์ค๋๊ฐ ์ง์ ํด๋ ์ธํฐํ์ด์ค๋ฅผ 
    ์ฐ๋ฆฌ๊ฐ ์๋ง๊ฒ ์ฌ์ ์ ํด์ค ์ผ๋ก์จ ์ด๋ฒคํธ ๋ฆฌ์ค๋๋ฅผ ์ค์ ํ๊ฒ ๋๋ค๊ณ  ํ๋ค.
    ๊ฐ๊ฐ onProgressChanger, onStartTrackingTouch, onStopTrackingTouch ์ธํฐํ์ด์ค ํจ์๋ฅผ ์ฌ์ ์ ํด์ฃผ์ด์ผ ํ๋ฉฐ
    ์ด๋ ๊ฐ๊ฐ ์์ ์ธ๊ธํ ๋์์ ๋ง์ถ์ด ์งํ๋๋ค.
  ```
+ onProgressChanged : ์ฌ์ฉ์ ํฐ์น์์ํด ์ํฌ๋ฐ๊ฐ ๋ณ๊ฒฝ๋  ๋
  ```KOTLIN
  * ์ ์ ๊ฐ thumb๋ฅผ ์์ง์ธ ๊ฒฝ์ฐ ํด๋นํ๋ progress๋ฅผ ๋จ์ ์๊ฐ์ผ๋ก ์ฌ์ค์ ํด์ค๋ค.
  * updateRemainTime(progress * 60 * 1000L) ์คํ

  private fun updateRemainTime(remainMillis: Long) {
      val remainSeconds = remainMillis / 1000

      remainMinutesTextView.text = "%02d'".format(remainSeconds / 60)
      remainSecondsTextView.text = "%02d".format(remainSeconds % 60)
  }
  ```
+ onStartTrackingTouch : ์ฌ์ฉ์๊ฐ ๋ฐ์ ์์ ๊ฐ์ ธ๋ค ๋๋ ์๊ฐ ์คํ
  ```KOTLIN
  * ์ํฌ๋ฐ ์กฐ์  ์ ์๋ก์ด ํ์ด๋จธ๋ฅผ ๋์์ํค๊ธฐ์ํด ์นด์ดํธ ๋ค์ด์ ๋ฉ์ถ๊ณ ,
    onStopTrackingTouch ์์ ํฐ์น๊ฐ ๋ฉ์ถ ๊ฒฝ์ฐ ์๋ก์ด ํ์ด๋จธ๋ฅผ ์์๋๋๋ก ํ๋ค.
  * stopCountDown()

  private fun stopCountDown() {
      currentCountDownTimer?.cancel()
      currentCountDownTimer = null
      soundPool.autoPause()
  } 
  ```
+ onStopTrackingTouch : ์ฌ์ฉ์๊ฐ ๋ฐ์์ ์์ ๋ผ๋ ์๊ฐ ์คํ
  ```KOTLIN
  // ์ด ๋ seekbar๊ฐ 0์ด๋ฉด stopCountDown()์, ๊ทธ๋ ์ง ์์ผ๋ฉด startCountDown()์ ์คํ
  
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
  
  // currentCounDownTimer ๋ CountDownTimer? ๊ฐ์ผ๋ก ์ด๊ธฐ๊ฐ null์ธ ์ ์ญ๋ณ์๋ก ์ ์ธํ ์ํ
  // ์ด๋ soundPool์ ๋๋ฐ์ด์ค ์์ฒด์ ์์ฒญํ๋ ๊ฒ์ด๊ธฐ ๋๋ฌธ์ ํ๋ฉด ์ข๋ฃ์์๋ ๊ณ์ ์ฌ์๋  ์ ์๋ค.
  // ๋๋ฌธ์ ์๋ช์ฃผ๊ธฐ์ ๋ฐ๋ฅธ ์ฒ๋ฆฌ๊ฐ ํ์ํ๋ค!
  
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
          
  // onTick() ์์ ํ์ด๋จธ๊ฐ ์๋ํ  ๋ ์ด๋ค ๋์์ ํ ์ง ์ค์ (๋จ์์๊ฐ, ์ํฌ๋ฐ๋ฅผ ๋ฐ๋ฆฌ์ด์ ๋ง๊ฒ ์ค์ )
  // onFinish() ์์ ์นด์ดํธ ๋ค์ด ์๋ฃ ์ฒ๋ฆฌ ํจ์๋ฅผ ํธ์ถ(completeCountDown())
  
  * updateRemainTime() ๊ณผ updateSeekBar ์์๋ ๋จ์ ๋ฐ๋ฆฌ์ด๋ฅผ ๊ธฐ์ค์ผ๋ก ํ์คํธ๋ทฐ์ ํ๋ก๊ทธ๋์ค๋ฐ๋ฅผ ์ค์ ํด์ค

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
  
  // tick ์ฌ์ด๋๋ฅผ ๋ฉ์ถ๊ณ  bell์ฌ์ด๋๋ฅผ ์คํ์ํด
  // tick ์ฌ์ด๋๋ loop ํ๋ผ๋ฏธํฐ๊ฐ -1๋ก ๊ณ์ ๋ฐ๋ณต๋๋ฉฐ, bell ์ฌ์ด๋๋ loop ํ๋ผ๋ฏธํฐ๊ฐ 0์ผ๋ก ํ๋ฒ๋ง ์คํ๋๋ค.
  ```
+ ์๋ช์ฃผ๊ธฐ์ ๋ฐ๋ผ soundPool ์ค์ 
  ```KOTLIN
  onResume() -> soundPool.autoResume()  // ์ฑ์ด ๋ค์ ์์
  onPause() -> soundPool.autoPause()    // ์ฑ์ด ํ๋ฉด์ ๋ณด์ด์ง ์์
  onDestroy() -> soundPool.release()    // ๋์ด์ ์ฑ์ ์ฌ์ฉํ์ง ์์ ๋ ์ฌ์ด๋ํ์ ๋ฉ๋ชจ๋ฆฌ์์ ํด์ 
  
  * soundPool load, play
  
    load() ๋ฉ์๋ : ์๋ฆฌํ์ผ์ ๋ก๋ํ์ฌ ๊ทธ ์์ด๋(soundId)๋ฅผ ๋ฐํ  
    play() ๋ฉ์๋ : ์๋ฆฌ๋ฅผ ์ฌ์  
    
    load()์ play()์ ๋ค์ด๊ฐ๋ ํ๋ผ๋ฏธํฐ์๋ 
    context, resId, priority, soundId, leftVolume, RightVolume, loop, rate ๋ฑ ์ด์์ผ๋ฉฐ, 
    ์ด๋ฅผํตํด ์ฌ์ํ  raw ๋๋ ํฐ๋ฆฌ์ mp4 ํ์ผ ๋ฆฌ์์ค๋ฅผ ์ง์ ํ๊ณ  ์ฌ์ํ๋ฉฐ, 
    ์์ชฝ ๋ณผ๋ฅจ์ ์ง์ ํ๊ณ , ์ฐ์ ์์(0์ด ๊ฐ์ฅ ๋ฎ์), 
    ๋ฐ๋ณต(0์ด๋ฉด ๋ฐ๋ณตํ์ง์๊ณ , -1์ด๋ฉด ๋ฐ๋ณต), ์ฌ์์๋(1.0๋ฐฐ์) ๋ฑ์ ์ค์ ํ  ์ ์๋ค. 
    ์ด์ธ์ ๋ค๋ฅธ ์ฌ๋ฌ๊ธฐ๋ฅ๋ค์ ๊ณต์๋ฌธ์ ์ฐธ์กฐ!
  ```     

๐ก ๋น๊ต์ ๋ฆฌ ํ์ํ ๋ด์ฉ๋ค  
```KOTLIN
์ด์ ์ ๋ถ์คํธ์ฝ์ค์์ ํ์ตํ AsycTask ์์ ์ฐ๋ ๋ํ์ฉํด์ progressbar๋ฅผ ๊ตฌํํ์์
Melon ํด๋ก ์ฝ๋ฉํ ๋ seekbar ์ฌ์ฉํ์๋๋ฐ ์์์ฌ์์ ๋ง์ถ์ด seekbar ์ด๋ํ๋๋ก ๊ตฌํํ์์
๋ณธ ํ๋ก์ ํธ ํ์ด๋ฒ์์ seekbar ์ฌ์ฉํ๋๋ฐ timer ํจ๊ป

์์ ์ธ๊ธํ ์ธ๋ถ๋ถ๋ค์๋ํด์ ๋ชํํ ๊ตฌ๋ถ์ง๊ณ  ์ ํด๋น๋ฐฉ์์ผ๋ก ๊ตฌํํ์ผ๋ฉฐ, ๋ฌด์จ์ฐจ์ด์ ์ด ์๋์ง ๋ฑ  
ํ์คํ๊ฒ ์์๋ณผ ํ์๊ฐ ์์๊ฑฐ ๊ฐ๋ค.
```
๐ก Kotlin์์ object ๋ก ์ ์ธํ๋ ์ด์ ?? 
```KOTLIN
object๋ก ์ ์ธํ๋ฉด ํด๋์ค ์ ์ธ๊ณผ ๋์์ ์ธ์คํด์ค(๊ฐ์ฒด)๊ฐ ์์ฑ๋๋ค๊ณ ํ๋ค.
object ๊ฐ์ฒด ์ญ์ ๋ค๋ฅธ class๋ฅผ ์์ํ๊ฑฐ๋ interface๋ฅผ ๊ตฌํํ ์ ์๋ค.
๐ฅ๐ฅ๐ฅ๐ฅ๐ฅ๐ฅ๐ฅ๐ฅ๐ฅ๐ฅ ๋ฐ๋์ ์ง๊ณ  ๋์ด๊ฐ ํ์๊ฐ ์์!!
์ฑ๊ธํค ํจํด, ํฉํ ๋ฆฌ ํจํด ๋ฑ์ ์ ์ฉํ๋ค๊ณ  ํ๋๋ฐ companion object์ ๋๋ถ์ด์ ํ๋ฃจ ๋ ์ก๊ณ  ๊ณต๋ถํด์ผ๊ฒ ๋ค.
์ด๋ถ๋ถ์ ์ถ๊ฐ์ ์ผ๋ก ๊ฒ์ํด์ ์์๋ด์ผํ ๊ฑฐ ๊ฐ๋ค. ์ ํด๋์ค ์ ์ธ๊ณผ ๋์์ ๊ฐ์ฒด๋ฅผ ์์ฑํด์ผํ๋์ง
๋ฑ ์ ํํ ๊ฐ์ฒด์ ํด๋์ค๋ ๋ญ์ง ๋ฑ ๋ญ๊ฐ ๋์ฌํ๋ ๋น ์ ธ์๋ ๊ธฐ๋ถ
```
