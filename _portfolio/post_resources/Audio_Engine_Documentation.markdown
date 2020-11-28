## Documentation
---

<a name="contents"></a>
### Contents
- [1 The SoundManager][sect-1]
	- [1.1  Initializing the Audio Engine](#sect-1.1 "Section 1.1")
	- [1.2  Uninitializing the Audio Engine](#sect-1.2 "Section 1.2")
	- [1.3  Shutting Down the Audio Engine](#sect-1.3 "Section 1.3")
- [2 Loading Wav Resources](#sect-2 "Section 2.0")
- [3 Creating Playlists](#sect-3 "Section 3.0")
- [4 Initializing a Sound Object](#sect-4 "Section 4.0")
- [5 Interacting with a GameSound](#sect-5 "Section 5.0")
- [6 Creating Callbacks](#sect-6 "Section 6.0")
- [7 Creating Sound Commands](#sect-7 "Section 7.0")
- [8 Misc.](#sect-8 "Section 8.0")
	- [8.1 The Sound Priority Table](#sect-8.1 "Section 8.1")
<br>
<br>
<br>
<br>


<a name="sect-1"></a>
## 1 - **The SoundManager**
- Singleton Sound Manager class -- The main interface for the user to interact with the audio engine.

<a id="sect-1.1"></a>
### 1.1 - Initializing the Audio Engine
> The AudioEngine must be initialized before any other interactions with the SoundManager.
>	
{% highlight cpp %}
//INITIALIZE SOUND MANAGER
	//contains audio engine and message queues
	//Launches and detaches AudioEngineThread
SoundManager::Create(); 
{% endhighlight %}

<a id="sect-1.2"></a>
### 1.2 - Uninitializing the Audio Engine
> The AudioEngine must be closed before the game application.
>
{% highlight cpp %}
//Called by Game Engine Game::Unload
	//shut down engine and Join AudioEngineThread to calling thread
SoundManager::CloseAudioEngineThread();
{% endhighlight %}

<a id="sect-1.3"></a>
### 1.3 - Shutting Down the Audio Engine
> The AudioEngine can also be shutdown by the user.
>
{% highlight cpp %}
//close AudioEngineThread and workers
SoundManager::QuitAudioEngine();
{% endhighlight %}

[back to contents](#contents "contents")

<br>

<a id="sect-2"></a>
## 2 - **Loading Wav Resources**
- This engine uses the XAudio2 Windows API, given a path to a .wav file and a _SoundID_ enum to associate with it, a _WaveSound_ is created in the audio engine, referencable by the _SoundID_.

> Wave Resources must be loaded into the audio engine before referenced. A custom _FileCallback_ can be given to SoundManager::LoadWaveResource as a way to attach custom code to be executed when the Wave Resource is loaded.
>	
{% highlight cpp %}
void LoadDemo1()
{
	bool sent = false;
	sent = SoundManager::LoadWaveResource("../MS2_AudioFiles/Fiddle_mono.wav", SoundID::PLAY_SOUND101);
	assert(sent);
	sent = SoundManager::LoadWaveResource("../MS2_AudioFiles/Bassoon_mono.wav", SoundID::PLAY_SOUND102);
	assert(sent);
	sent = SoundManager::LoadWaveResource("../MS2_AudioFiles/Oboe_mono.wav", SoundID::PLAY_SOUND103);
	assert(sent);
	sent = SoundManager::LoadWaveResource("../MS2_AudioFiles/SongA.wav", SoundID::PLAY_SOUND104);
	assert(sent);
	sent = SoundManager::LoadWaveResource("../MS2_AudioFiles/SongB.wav", SoundID::PLAY_SOUND105, new Demo1_FileCallback());
	assert(sent);
}
{% endhighlight %}

[back to contents](#contents "contents")

<br>


<a id="sect-3"></a>
## 3 - **Creating Playlists**
- After loading all needed wave resources, a playlist can be created to chain together _WaveSound_'s.

> A playlist is created by supplying the total count and _SoundID_ of each sound to SoundManager::CreateGamePlaylist as well as associating it to a _PlaylistID_ or string.
>	
{% highlight cpp %}
void Demo2()
{
	bool sent = false;
	sent = SoundManager::CreateGamePlaylist("Seinfeld_Song", 8, SoundID::PLAY_SOUND_INTRO, SoundID::PLAY_SOUND_A, SoundID::PLAY_SOUND_ATOB,
		SoundID::PLAY_SOUND_B, SoundID::PLAY_SOUND_BTOC, SoundID::PLAY_SOUND_C, SoundID::PLAY_SOUND_CTOA, SoundID::PLAY_SOUND_END);
	...


{% endhighlight %}

[back to contents](#contents "contents")

<br>


<a id="sect-4"></a>
## 4 - **Initializing a Sound Object**
- After loading all the wave resource, a _Sound_ can be created to play an manipulate a particular _WaveSound_.

> A reference to a sound handle is created by supplying the _SoundID_ to SoundManager::InitializeSound. This function must also be supplied a _GameSound_ as an out parameter, used to give access to a _Sound_.
>	
{% highlight cpp %}
void Demo1()
{
	bool sent = false;

	{
		GameSound gSnd_101;
		sent = SoundManager::InitializeSound(gSnd_101, SoundID::PLAY_SOUND101, new CustomSoundCallback());
		assert(sent);
	...


{% endhighlight %}


>In addition, a CustomCallback can be supplied to allow for custom code to be executed on the following _Sound_ events: 
- sound stopped
- sound ended
- sound released
- sound played
- sound paused
- sound resumed
- sound killed.
>

[back to contents](#contents "contents")

<br>


<a id="sect-5"></a>
## 5 - **Interacting with a GameSound**
- After initializing your _GameSound_ with a active _Sound_ handle through SoundManager::InitializeSound, the associated _WaveSound_ can be played and manipulated through the _GameSound_ object member functions.

> Numerous actions can be called on a sound, including: 
- play
- pause
- stop
- set volume
- ramp the volume over time
- set pan
- change pan over time
- set pitch
- get current playtime
- add scripts

>	
{% highlight cpp %}
void Demo1()
{
	bool sent = false;

	{
		GameSound gSnd_101;
		sent = SoundManager::InitializeSound(gSnd_101, SoundID::PLAY_SOUND101, new CustomSoundCallback());
		assert(sent);
	...


{% endhighlight %}


[back to contents](#contents "contents")

<br>


[sect-1]: #sect-1 "Section 1.0"
[sect-0]: #sect-0 "Section 0.0"

