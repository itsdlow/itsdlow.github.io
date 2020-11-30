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
- [6 Callbacks](#sect-6 "Section 6.0")
	- [6.1  FileCallback](#sect-6.1 "Section 6.1")
	- [6.2  SoundCallback](#sect-6.2 "Section 6.2")
	- [6.3  Creating Callbacks](#sect-6.3 "Section 6.3")
- [7 Sound Commands](#sect-7 "Section 7.0")
	- [7.1 Creating GameCommands](#sect-7.1 "Section 7.1")
	- [7.2 Creating SoundScripts](#sect-7.2 "Section 7.2")
- [8 Miscellaneous](#sect-8 "Section 8.0")
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

> A reference to a sound handle is created by supplying the _SoundID_ or _PlaylistID_ to SoundManager::InitializeSound. This function must also be supplied a _GameSound_ as an out parameter, used to give access to a _Sound_.
>	
{% highlight cpp %}
void Demo1()
{
	bool sent = false;

	{
		GameSound gSnd_101;
		sent = SoundManager::InitializeSound(gSnd_101, SoundID::PLAY_SOUND101);
		assert(sent);
	...


{% endhighlight %}

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
bool PlayAndReleaseSound(SoundID id, int priority, float vol)
{
	GameSound gSnd;
	const bool sent = SoundManager::InitializeSound(gSnd, id);
	assert(sent);
	assert(Handle::Status::SUCCESS == gSnd.SetVolume(vol));

	const Handle::Status status = gSnd.Play(priority);//Lower priority returns insufficient space handle status
	assert(Handle::Status::SUCCESS == status || Handle::Status::INSUFFIENT_SPACE == status);

	return sent;
}

{% endhighlight %}


[back to contents](#contents "contents")

<br>


<a id="sect-6"></a>
## 6 - **Callbacks**
- There are 2 places where a callback can be supplied, when initializing a _WaveSound_ or a _Sound_.  



<a id="sect-6.1"></a>

### 6.1 - FileCallbacks
> A _FileCallback_ can be supplied when intializing a _WaveSound_. This enables the user to execute custom code when the following _WaveSound_ load events occur:
- wave already loaded
- wave load error
- wave loaded
>

{% highlight cpp %}
void LoadDemo5()
{
	bool sent = false;
	sent = SoundManager::LoadWaveResource("../MS2_AudioFiles/Electro_mono.wav", SoundID::PLAY_SOUND501);
	assert(sent);
	sent = SoundManager::LoadWaveResource("../MS2_AudioFiles/Alert_mono.wav", SoundID::PLAY_SOUND502, new Demo5_FileCallback());
	assert(sent);
}


{% endhighlight %}


<a id="sect-6.2"></a>

### 6.2 - SoundCallbacks
> A _SoundCallback_ can be supplied when intializing a _Sound_. This enables the user to execute custom code when the following _Sound_ events occur:
- sound stopped
- sound ended
- sound released
- sound played
- sound paused
- sound resumed
- sound killed.
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


<a id="sect-6.3"></a>

### 6.3 - Creating Callbacks
> A custom _SoundCallback_ or _FileCallback_ can be created by simply defining a class which publically inherits from either and overriding the relevant methods.
>


[back to contents](#contents "contents")

<br>


<a id="sect-7.0"></a>
## 7 - **Sound Commands**
- A sound command is used to trigger a sound to play or an action on a particular sound. There are 2 types of sound commands, a _GameCommand_ and a _SoundScript_.

<a id="sect-7.1"></a>
### 7.1 - Creating GameCommands
> The first derived sound command is a _GameCommand_, this allows for execution of a command with user supplied code, at a given delta time. This is done by calling SoundManager::CreateTimeEvent, supplying a delta time for execution as well as a derived _GameCommand_, initialized through RAII.

{% highlight cpp %}

	//create Sound events
	sent = SoundManager::CreateTimeEvent(new CustomGameCommand(SoundID::PLAY_SOUND502, 0.3f, -1.0f), 5 * Time(Duration::TIME_ONE_SECOND));
	...

{% endhighlight %}


<a id="sect-7.2"></a>
### 7.2 - Creating SoundScripts
> The second derived sound command is a _SoundScript_, this allows for execution of a command with user supplied code, at a given delta time *on* a particular _GameSound_. This is done by calling GameSound::AddScript, supplying a delta time for execution as well as a derived _SoundScript_, initialized through RAII.

{% highlight cpp %}

void Demo5_Beethoven(const Time& load_start_time)
{
	SoundManager::StopAllSounds();
	const Time elapsedTime = SoundManager::GetSoundCurrentTime() - load_start_time;
	//delta Time of TIME since load UNDER 60s
	const Time deltaTime = (60 * Time(Duration::TIME_ONE_SECOND)) - elapsedTime;
	
	GameSound gSnd;
	const bool sent = SoundManager::InitializeSound(gSnd, SoundID::PLAY_SOUND503);
	assert(sent);
	Handle::Status status = gSnd.Play();
	assert(Handle::Status::SUCCESS == status || Handle::Status::INSUFFIENT_SPACE == status);

	// set stop command @ 60 seconds from DEMO_START
	status = gSnd.AddScript(new StopSoundScript(), deltaTime);
	assert(Handle::Status::SUCCESS == status);
}

{% endhighlight %}


[back to contents](#contents "contents")

<br>


<a id="sect-8.0"></a>
## 8 - **Miscellaneous**

<a id="sect-8.1"></a>
### 8.1 - The Sound Priority Table
> A sound priority table has been implemented which restricts the number of sounds allowed to play at once to a set, configurable amount. A _Sound_ is given a priority number on initialization, determining its rank in the table. If a new _Sound_ is played while the priority table is full, the lowest priority _Sound_ is "killed".

[back to contents](#contents "contents")

<br>

[sect-1]: #sect-1 "Section 1.0"
[sect-0]: #sect-0 "Section 0.0"

