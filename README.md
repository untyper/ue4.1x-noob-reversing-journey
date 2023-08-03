# UE4.1x Noob Reversing Journey

<div id="post_message_3030862"><b>INTRODUCTION</b><br>
<br>
Hi guys,<br>
<br>
First things first, I'm Italian and my english can be very bad, please excuse me.<br>
<br>
Second, this will be a very long read, I do this to help myself and I hope even someone else.<br>
Repeating all and writing it down is just a way to imagazine info for me.<br>
<br>
Third, don't know why the images can't load.<br>
<br>
If you want just to help me, thanks and please jump directly at the end where there are my questions.<br>
<br>
Here a lot of info on why I'm here, what I want to achieve, mainly implemented to let you know why I'm even writing this post (you can skip, I wont blame you):<br>
<br>
<div style="margin:20px; margin-top:5px">
<div class="smallfont" style="margin-bottom:2px">
<input type="button" value="Hide Spoiler!" style="width:100px;font-size:14px;font-bold:true;margin:10px;padding:0px;" onclick="if (this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display != '') 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = ''; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = 'none'; 
this.value = 'Hide Spoiler!'; 
} 
else 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = 'none'; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = ''; 
this.value = 'Show Spoiler!'; 
}">
<div id="show_spoil" style="margin: 0px; border-style: solid; border-width: 1px; padding: 4px; width: 98%;">
<br>
I'm a UE4 Gameplay programmer from 6 months, made a couple of projects for myself to start looking for a job.<br>
I know how the engine works at the top level, but know nothing on how the engine works on low level. Pretty good on C++.<br>
<br>
This could piss off a lot of people but I am not really interested in Game Hacking on a general level, I don't want to make cheats, but lately I had the impulse to make Mods.<br>
<br>
I've approached this whole thing for a basic reason: sometime I play games in which, being a game developer myself, I start to wonder: "If I were the developer I would have implemented this mechanic in this way".<br>
<br>
This happened with 2 main games recently: <br>
- Cyberpunk (but just for the will of putting some fixes tbh, poor devs),<br>
- FFVII Remake (FFVII for PS1 is my fav game of all time).<br>
<br>
I started with a lot of basics guides here, on the other famous forum and YT, did a lot of Cheat Engine and Assault Cube these weeks.<br>
<br>
Joined Cyberpunk discord before Christmas while starting to do some tuts here and there and ... shit, those people are on another level, maybe I could be of help with 6 months of studying. <br>
<br>
So I've switched very fast to my next idea: FFVII.<br>
The game should come out on April, and I have a few months to get ready to know how I could implement the things I have in my mind. Plus is made with UE4, a Engine I already use, this is perfect!<br>
</div>
<div id="hide_spoil" style="display: none;">
</div>
</div>
</div><br>
<br>
So I started to search how to mod UE4 Games, discovered that before modding them you have to reverse them, did some other research and now I think to have a pretty clear idea on how to proceed, I'll Implement the steps as I go forward.<br>
<br>
<b>JOURNEY</b><br>
<br>
<div style="margin:20px; margin-top:5px">
<div class="smallfont" style="margin-bottom:2px">
<input type="button" value="Hide Spoiler!" style="width:100px;font-size:14px;font-bold:true;margin:10px;padding:0px;" onclick="if (this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display != '') 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = ''; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = 'none'; 
this.value = 'Hide Spoiler!'; 
} 
else 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = 'none'; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = ''; 
this.value = 'Show Spoiler!'; 
}">
<div id="show_spoil" style="margin: 0px; border-style: solid; border-width: 1px; padding: 4px; width: 98%;">
<br>
<b>STEP 1: FINDING GNames &amp;&amp; GObjects</b><br>
<br>
<div style="margin:20px; margin-top:5px">
<div class="smallfont" style="margin-bottom:2px">
<input type="button" value="Hide Spoiler!" style="width:100px;font-size:14px;font-bold:true;margin:10px;padding:0px;" onclick="if (this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display != '') 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = ''; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = 'none'; 
this.value = 'Hide Spoiler!'; 
} 
else 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = 'none'; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = ''; 
this.value = 'Show Spoiler!'; 
}">
<div id="show_spoil" style="margin: 0px; border-style: solid; border-width: 1px; padding: 4px; width: 98%;">
<br>
Every Unreal Game has 2 very important variables that should help me proceed on my journey:<br>
<br>
-GNames is a TArray of Unicode Strings<br>
-GObject is a TArray of Class Pointers<br>
<br>
With GObjects I should have access to most (all?) objects in the game, with GNames I should know what they are.<br>
These infos will help me build an SDK to mod the game.<br>
<br>
So, how to find them? Need to start practice!<br>
</div>
<div id="hide_spoil" style="display: none;">
</div>
</div>
</div><br>
<blockquote><br>
<b>STEP 1-a: GNames, JUMPER &amp;&amp; FPS TEMPLATE</b><br>
<div style="margin:20px; margin-top:5px">
<div class="smallfont" style="margin-bottom:2px">
<input type="button" value="Hide Spoiler!" style="width:100px;font-size:14px;font-bold:true;margin:10px;padding:0px;" onclick="if (this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display != '') 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = ''; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = 'none'; 
this.value = 'Hide Spoiler!'; 
} 
else 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = 'none'; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = ''; 
this.value = 'Show Spoiler!'; 
}">
<div id="show_spoil" style="margin: 0px; border-style: solid; border-width: 1px; padding: 4px; width: 98%;">
<br>
I've found here on the forum a post that talked about Jumper <b>~removed by staff~</b>, free, simple, a little boring, and made with UE4, downloaded.<br>
<br>
One thing I know about GNames: they look like "None, ByteProperty, someProperty ecc". <br>
Not much, but better than nothing.<br>
<br>
There are a lot of info on how to find GNames but I found mainly 3 ways of doing that:<br>
- Analyzing the EXE with sigs (array of bytes that should be almost identical in every game)<br>
- Reversing via Source Code and IDA<br>
- Using fast methods that other people found for me.<br>
<br>
<b>EASY METHOD</b><br>
<br>
Started with the easy way, from a YT video the steps are very simple.<br>
- Open Cheat Engine<br>
- Attach to Jumper<br>
- Search the String "MulticastDelegateProperty"<br>
- Browse memory regions of the found addresses, and find the one in which you read something like "None, ByteProperty, someProperty ecc" scrolling up a bit from where the windows open - 3 results, and the first worked for me:<br>
<br>
	
![Alt 1-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/1.jpg)

<br>
- Like you can see I have 16 blank bytes before "None". Find the address of the first byte of the first 8 blank bytes before "None"<br>
- Search it as 8 bytes HEX, if you find nothing, try the 8 blank bytes before<br>
- Now just follow back all the pointers you find till you have 2 static addresses - pretty easy, after 2 mins: <br>
<br>

![Alt 2-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/2.jpg)

<br>
- You want to put those offsets in ReClass and use the one that has 2 pointers as first entries:<br>
<br>

![Alt 3-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/3.jpg)

<br>
- Follow the first pointer and:<br>
<br>

![Alt 4-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/4.jpg)

<br>
- That was easy, apparently this is what I need, have I learned something? <br>
<br>
<b>No.</b><br>
<br>
But, I have a offset now: 21DD6B8.<br>
<br>
<b>IDA &amp;&amp; SOURCE</b><br>
<br>
Let's see if I can find the same info using Source and IDA. Jumper uses UE4.10, I've seen this by simply viewing the proprieties of the EXE.<br>
<br>
Here it is in "UnrealNames.cpp":<br>
<br>

```c++
TNameEntryArray& FName::GetNames()
{
	static TNameEntryArray*	Names = NULL;
	if( Names == NULL )
	{
		check(IsInGameThread());
		Names = new TNameEntryArray();
	}
	return *Names;
}
```
  
Searching for the call at GetNames() in this file led me here (line 678)<br>
<br>

```c++

	FNameEntry* OldHash=NameHash[iHash];
	TNameEntryArray& Names = GetNames();
	if (OutIndex < 0)
	{
		OutIndex = Names.AddZeroed(1);
	}
	else
	{
		check(OutIndex < Names.Num());
	}
	FNameEntry* NewEntry = AllocateNameEntry( InName, OutIndex, OldHash, FNameInitHelper<TCharType>::IsAnsi );
	if (FPlatformAtomics::InterlockedCompareExchangePointer((void**)&Names[OutIndex], NewEntry, NULL) != NULL) // we use an atomic operation to check for unexpected concurrency, verify alignment, etc
	{
		UE_LOG(LogUnrealNames, Fatal, TEXT("Hardcoded name '%s' at index %i was duplicated (or unexpected concurrency). Existing entry is '%s'."), *NewEntry->GetPlainNameString(), NewEntry->GetIndex(), *Names[OutIndex]->GetPlainNameString() );
	}
	if (FPlatformAtomics::InterlockedCompareExchangePointer((void**)&NameHash[iHash], NewEntry, OldHash) != OldHash) // we use an atomic operation to check for unexpected concurrency, verify alignment, etc
	{
		check(0); // someone changed this while we were changing it
	}
	check(OutIndex >= 0);
	return true;
}
```

That's juicy, search in IDA the string "Hardcoded name '%s' at index %i was duplicated (or unexpected concurrency). Existing entry is '%s'."<br>
Follow the XRef, decompile and let's see what we got. Right above the string I can read very clearly "_InterlockedCompareExchenge64", 2 times.<br>
<br>

![Alt 5-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/5.jpg)

<br>
I can see those line also in the source, and GetNames() is even more far up. So let's scroll up.<br>
<br>

![Alt 6-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/6.jpg)

<br>
Wait... can you see 3 times "qword_1421DD6B8"?<br>
Remember the offset before? 21DD6B8!<br>
IDA starts with the base address at 14000000! That's it!<br>
<br>
Am I done? Boh.<br>
<br>
I was confused though: I was searching for GetNames(): a function and that was not a function.<br>
In IDA functions are like "sub_XXXXXXXX", I started clicking on all function near that point but no luck <img src="https://www.unknowncheats.me/forum/images/smilies/sad.gif" border="0" alt="" title="Frown" class="inlineimg"><br>
Clicking on the qword itself brought me here, and the function on that line (sub_1401BD5C0) was the same I've already found in the pseudocode with no luck.<br>
<br>

![Alt 7-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/7.jpg)

<br>
Now, I don't know really what I have done here and I'm hoping someone can clear my mind, but here it comes the illumination. <br>
Remeber in Cheat Engine? When we grabbed the offset, we grabbed the address 16 bytes before the "None".<br>
16 bytes, that's 10 in HEX, 21DD6B8 + 10 = 21DD6C8!<br>
In the image you can see that at that adrees there is another function: sub_1401BD490!<br>
<br>
Clicked it, F5, and discovered that the first thing it does is call another function: sub_1401DA190.<br>
<br>

![Alt 8-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/8.jpg)

<br>
Clicked it, scrolled down a bit and... <img src="https://www.unknowncheats.me/forum/images/smilies/You_Rock_Emoticon.gif" border="0" alt="" title="You Rock Emoticon" class="inlineimg"><br>
<br>

![Alt 9-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/9.jpg)

<br>
Interesting that it calls sub_1401BD490 on every Name, I looked a little bit at source code but I didn't understand exactly what I was looking.<br>
Again, if you want you can clear my mind.<br>
At least, something important learned, GNames are "offseted" (I'm writing too much, now I come up with new words) by 10. Better keep in mind that.<br>
<br>
<b>SIGS &amp;&amp; PDB</b><br>
<br>
Ok now, let'see this signatures.<br>
From what I understand, once I have found Gnames, I can take the array of bytes and compare it with others, thing is, I don't have other games, well... let's make one!<br>
<br>
Downloaded UE4.10 and cooked the FPS Template with PDB.<br>
Opened in IDA, and it's to easy, just search for it. From a YT video I heard to take the bytes from the "mov" to the "jnz". I'll highlight them for you in the pic.<br>
<br>

![Alt 10-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/10.jpg)

<br>
48 8B 05 B5 8F 1B 02 48 85 C0 75 50<br>
<br>
That's our array!<br>
<br>
Let's look at Jumper now.<br>
Oh... that's a problem, none of the function I found look even similar to the one from the Template. I was all happy with emoticon and stuff, but maybe I wasn't even looking at GNames this whole time. <br>
<br>
<img src="https://www.unknowncheats.me/forum/images/smilies/wtf.gif" border="0" alt="" title="Wtf" class="inlineimg"><br>
<br>
It' 4 AM, I'll call it a day, any advice is welcomed <img src="https://www.unknowncheats.me/forum/images/smilies/big_smile.png" border="0" alt="" title="Smilie" class="inlineimg"><br>
</div>
<div id="hide_spoil" style="display: none;">
</div>
</div>
</div><br>
<br>
<b>STEP 1-b: GNames, JUMPER &amp;&amp; FPS TEMPLATE - Was I looking at GNames? - Quick Update 08/01</b><br>
<br>
<div style="margin:20px; margin-top:5px">
<div class="smallfont" style="margin-bottom:2px">
<input type="button" value="Hide Spoiler!" style="width:100px;font-size:14px;font-bold:true;margin:10px;padding:0px;" onclick="if (this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display != '') 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = ''; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = 'none'; 
this.value = 'Hide Spoiler!'; 
} 
else 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = 'none'; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = ''; 
this.value = 'Show Spoiler!'; 
}">
<div id="show_spoil" style="margin: 0px; border-style: solid; border-width: 1px; padding: 4px; width: 98%;">
<br>
I know you bastards are probably laughing at me!<br>
But I have a PDB!<br>
The question is: Was I looking at GNames?<br>
Well, just let's see in the Template Game what I was looking!<br>
<br>
I have redone all the steps that I have done in Jumper in the Template and here we are.<br>
<br>
	
![Alt 11-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/11.jpg)

<br>
To begin, no sign of GetNames even with the PDB, but in the source is there, just after FName::Hash() <img src="https://www.unknowncheats.me/forum/images/smilies/sad.gif" border="0" alt="" title="Frown" class="inlineimg"><br>
This is bad, why the source tell me lies <img src="https://www.unknowncheats.me/forum/images/smilies/sad.gif" border="0" alt="" title="Frown" class="inlineimg"><br>
<br>
And:<br>
- sub_1401BD5C0 is FName::InitInternal_FindOrAddNameEntry()<br>
- sub_1401BD490 is FName::InitInternal()<br>
- sub_1401DA190 is FName::StaticInit()<br>
<br>
So the answer is: No moron, you wasn't looking at GetNames().<br>
<br>
I'm out of ammo here, seems that I have picked the wrong literal string.<br>
</div>
<div id="hide_spoil" style="display: none;">
</div>
</div>
</div><br>
<br>
<b>STEP 1-c: Time for GObjects - Apparently the offset is good <img src="https://www.unknowncheats.me/forum/images/smilies/smile.gif" border="0" alt="" title="Big Grin" class="inlineimg"> - Update 09/01</b><br>
<br>
<div style="margin:20px; margin-top:5px">
<div class="smallfont" style="margin-bottom:2px">
<input type="button" value="Hide Spoiler!" style="width:100px;font-size:14px;font-bold:true;margin:10px;padding:0px;" onclick="if (this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display != '') 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = ''; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = 'none'; 
this.value = 'Hide Spoiler!'; 
} 
else 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = 'none'; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = ''; 
this.value = 'Show Spoiler!'; 
}">
<div id="show_spoil" style="margin: 0px; border-style: solid; border-width: 1px; padding: 4px; width: 98%;">
<br>
So I have done research and I have understood something but I have not understood the fact that GetNames() is missing in IDA.<br>
I'll make this one the first question for you.<br>
<br>
But, getting to what I have understood, the offset of GNames I have seems very good since it looks like a tons of others on the web.<br>
I just need to see if it wil work, but for that I need GObjects!<br>
<br>
What I know of GObjects? Nothing really, at least with GNames we had a clear sign it was it, the None, ByteProperty ecc.<br>
Here nothing. One thing I noticed though, in reclass there are always some "FF" in the video I watched.<br>
<br>
Ok the methods are the same:<br>
- Analyzing the EXE with sigs (array of bytes that should be almost identical in every game)<br>
- Reversing via Source Code and IDA<br>
- Using fast methods that other people found for me.<br>
<br>
<b>Unreal Finder Tool</b><br>
<br>
This time I will start with an other easy way though, UFT by CorrM, so his tool gives me offset 21EDE80. Let's Compare using source and IDA.<br>
There is nothing to say here, if you want to know how to use it just watch his video.<br>
<br>
<b>IDA &amp;&amp; SOURCE</b><br>
<br>
Source, UObjectHash.cpp:
<br>
	
```c++
FUObjectArray& GetUObjectArray()
{
	static FUObjectArray GlobalUObjectArray;
	return GlobalUObjectArray;
}
 ```

Find ref, find literals, you know how it works, I'm using "Object not found" from UGameViewportClient::HandleDisplayAllCommand().<br>
<br>
4 results, we can do this.<br>
<br>
The first has something weird:<br>
<br>

```c++

            v12 = v16;
          sub_1401AA950(a3, L"Property '%s' not found on object '%s'", v19, v12);
          if ( v16 )
            sub_140157CF0(v16);
        }
        else
        {
          v10 = (__int64 *)(*(_QWORD *)(a1 + 64) + 32i64 * (int)sub_140D47260(a1 + 64, 1i64));
          *v10 = v8;
          v10[2] = v14;
        }
      }
      else
      {
        sub_1401AA950(a3, L"Object not found");
      }
    }
  }
  return 1;
}
```

There isn't any "Property '%s' not found on object '%s'" in my function. Let' search this in source.<br>
<br>
Found just one result! If there is also here the GetUObjectArray() we can use this!<br>
<br>
Source:<br>
<br>

```c++
bool UGameViewportClient::HandleDisplayCommand( const TCHAR* Cmd, FOutputDevice& Ar )
{
	TCHAR ObjectName[256];
	TCHAR PropStr[256];
	if ( FParse::Token(Cmd, ObjectName, ARRAY_COUNT(ObjectName), true) &&
		FParse::Token(Cmd, PropStr, ARRAY_COUNT(PropStr), true) )
	{
		UObject* Obj = FindObject<UObject>(ANY_PACKAGE, ObjectName);
		if (Obj != NULL)
		{
			FName PropertyName(PropStr, FNAME_Find);
			if (PropertyName != NAME_None && FindField<UProperty>(Obj->GetClass(), PropertyName) != NULL)
			{
				FDebugDisplayProperty& NewProp = DebugProperties[DebugProperties.AddZeroed()];
				NewProp.Obj = Obj;
				NewProp.PropertyName = PropertyName;
			}
			else
			{
				Ar.Logf(TEXT("Property '%s' not found on object '%s'"), PropStr, *Obj->GetName());
			}
		}
		else
		{
			Ar.Logf(TEXT("Object not found"));
		}
	}
 
	return true;
}
```

Nope <img src="https://www.unknowncheats.me/forum/images/smilies/sad.gif" border="0" alt="" title="Frown" class="inlineimg"> Let's try the others. <br>
Fastforward: All 3 that remains could be my function.<br>
<br>
Let's try finding "Object not found" in the source.<br>
Yep, 4 results in fact, all in GameViewPortClient.cpp<br>
<br>
The first one is HandleDisplayCommand() and there isn't our function there.<br>
<br>
All the others have it though, those are HandleDisplayAllCommand(), HandleDisplayAllLocationCommand() and HandleDisplayAllRotationCommand().<br>
<br>
The last 2 are pratically identical, the other one has an if statement extra.<br>
If I find the one that differs in IDA, i know I can use either one of the remaining ones. Fastest thought: let's compare how many lines of code there are:<br>
<br>
- sub_140C658D0 308 lines<br>
- sub_140C65EB0 126 lines<br>
- sub_140C661A0 126 lines<br>
<br>
Bingo! I can use either one of the latters and it will be or HandleDisplayAllLocationCommand() or HandleDisplayAllRotationCommand().<br>
They are identical so I don't care, let's take HandleDisplayAllLocationCommand() and sub_140C661A0.<br>
<br>
Source:<br>
<br>

```c++
bool UGameViewportClient::HandleDisplayAllLocationCommand( const TCHAR* Cmd, FOutputDevice& Ar )
{
	TCHAR ClassName[256];
	if (FParse::Token(Cmd, ClassName, ARRAY_COUNT(ClassName), true))
	{
		UClass* Cls = FindObject<UClass>(ANY_PACKAGE, ClassName);
		if (Cls != NULL)
		{
			// add all un-GCable things immediately as that list is static
			// so then we only have to iterate over dynamic things each frame
			for (TObjectIterator<UObject> It(true); It; ++It)
			{
				if (!GetUObjectArray().IsDisregardForGC(*It))
				{
					break;
				}
				else if (It->IsA(Cls))
				{
					FDebugDisplayProperty& NewProp = DebugProperties[DebugProperties.AddZeroed()];
					NewProp.Obj = *It;
					NewProp.PropertyName = NAME_Location;
					NewProp.bSpecialProperty = true;
				}
			}
			FDebugDisplayProperty& NewProp = DebugProperties[DebugProperties.AddZeroed()];
			NewProp.Obj = Cls;
			NewProp.PropertyName = NAME_Location;
			NewProp.bSpecialProperty = true;
		}
		else
		{
			Ar.Logf(TEXT("Object not found"));
		}
	}
 
	return true;
}
```

IDA:<br>
<br>

```c++
char __fastcall sub_140C661A0(__int64 a1, __int64 a2, __int64 a3, __int64 a4)
{
  __int64 v6; // rax
  __int64 v7; // r12
  __int64 v8; // rax
  __int64 v9; // r8
  __int64 v10; // rsi
  int v11; // er15
  int v12; // edi
  int v13; // ebp
  __int64 v14; // r14
  __int64 v15; // rbx
  __int64 v16; // rdx
  __int64 v17; // rcx
  int v18; // edx
  int v19; // eax
  int v20; // ecx
  int v21; // eax
  int v22; // ecx
  __int64 v23; // rbx
  __int64 v24; // rdx
  __int64 v25; // rcx
  int v26; // eax
  __int64 v27; // rcx
  __int64 v28; // rax
  __int64 v29; // rcx
  __int64 v30; // rcx
  __int64 v32; // [rsp+28h] [rbp-270h] BYREF
  __int64 v33; // [rsp+30h] [rbp-268h] BYREF
  int v34; // [rsp+38h] [rbp-260h]
  int v35; // [rsp+48h] [rbp-250h]
  char v36[512]; // [rsp+50h] [rbp-248h] BYREF
 
  v32 = a2;
  LOBYTE(a4) = 1;
  if ( (unsigned __int8)sub_1401B70C0(&v32, v36, 256i64, a4) )
  {
    v6 = sub_14020CB90(L"/Script/CoreUObject");
    v7 = sub_1402766C0(v6, -1i64, v36, 0i64);
    if ( v7 )
    {
      v8 = sub_14027A6E0(L"/Script/CoreUObject");
      LOBYTE(v9) = 1;
      sub_1401FEFE0(&v33, v8, v9, 16i64);
      v10 = v33;
      v11 = v35;
      v12 = v34;
LABEL_4:
      while ( v12 < *(_DWORD *)(v10 + 4112) )
      {
        if ( v12 < 0 )
          break;
        v13 = v12 / 0x4000;
        v14 = v12 % 0x4000;
        v15 = *(_QWORD *)(*(_QWORD *)(v10 + 8i64 * (v12 / 0x4000) + 16) + 8 * v14);
        if ( *(_DWORD *)(v15 + 12) > GetUObjectArray()[1] )
          break;
        if ( (unsigned int)(*(_DWORD *)(*(_QWORD *)(*(_QWORD *)(*(_QWORD *)(v10 + 8i64 * v13 + 16) + 8 * v14) + 16i64)
                                      + 136i64)
                          - *(_DWORD *)(v7 + 136)) <= *(_DWORD *)(v7 + 140) )
        {
          v16 = *(_QWORD *)(a1 + 64) + 32i64 * (int)sub_140D47260(a1 + 64, 1i64);
          v17 = *(_QWORD *)(*(_QWORD *)(v10 + 8i64 * v13 + 16) + 8 * v14);
          *(_DWORD *)(v16 + 24) |= 1u;
          *(_QWORD *)(v16 + 16) = 249i64;
          *(_QWORD *)v16 = v17;
        }
        v18 = *(_DWORD *)(v10 + 4112);
        do
        {
          if ( ++v12 >= v18 )
            break;
          while ( 1 )
          {
            v19 = v12;
            v20 = v12 & 0x3FFF;
            if ( v12 < 0 )
            {
              v19 = v12 + 0x3FFF;
              v20 -= 0x4000;
            }
            if ( *(_QWORD *)(*(_QWORD *)(v10 + 8i64 * (v19 >> 14) + 16) + 8i64 * v20) )
              break;
            if ( ++v12 >= v18 )
              goto LABEL_4;
          }
          v21 = v12;
          v22 = v12 & 0x3FFF;
          if ( v12 < 0 )
          {
            v21 = v12 + 0x3FFF;
            v22 -= 0x4000;
          }
        }
        while ( (v11 & *(_DWORD *)(*(_QWORD *)(*(_QWORD *)(v10 + 8i64 * (v21 >> 14) + 16) + 8i64 * v22) + 8i64)) != 0 );
      }
      v23 = *(int *)(a1 + 72);
      v24 = *(unsigned int *)(a1 + 76);
      v25 = (unsigned int)(v23 + 1);
      *(_DWORD *)(a1 + 72) = v25;
      if ( (int)v25 > (int)v24 )
      {
        v26 = sub_14011BA90(v25, v24, 32i64);
        *(_DWORD *)(a1 + 76) = v26;
        v27 = *(_QWORD *)(a1 + 64);
        if ( v27 || v26 )
          *(_QWORD *)(a1 + 64) = sub_140165C50(v27, 32i64 * v26, 0i64);
      }
      v28 = *(_QWORD *)(a1 + 64);
      v29 = 32 * v23;
      *(_QWORD *)(v29 + v28) = 0i64;
      *(_QWORD *)(v29 + v28 + 8) = 0i64;
      *(_QWORD *)(v29 + v28 + 16) = 0i64;
      *(_QWORD *)(v29 + v28 + 24) = 0i64;
      v30 = *(_QWORD *)(a1 + 64) + 32 * v23;
      *(_DWORD *)(v30 + 24) |= 1u;
      *(_QWORD *)v30 = v7;
      *(_QWORD *)(v30 + 16) = 249i64;
    }
    else
    {
      sub_1401AA950(a3, L"Object not found");
    }
  }
  return 1;
}
```

Here I made one mistake initially, I started to analyze the code from the bottom, and there is a while loop that can trick you, leading you to guess that sub_14011BA90 could be GetObjects() and sub_140165C50 AddZeroed(), but once analyzed was pretty obvious they were not.<br>
Restarted from the top I ended up with these comments:<br>
<br>

```c++
char __fastcall sub_140C661A0(__int64 a1, __int64 a2, __int64 a3, __int64 a4)
{
  __int64 v6; // rax
  __int64 v7; // r12
  __int64 v8; // rax
  __int64 v9; // r8
  __int64 v10; // rsi
  int v11; // er15
  int v12; // edi
  int v13; // ebp
  __int64 v14; // r14
  __int64 v15; // rbx
  __int64 v16; // rdx
  __int64 v17; // rcx
  int v18; // edx
  int v19; // eax
  int v20; // ecx
  int v21; // eax
  int v22; // ecx
  __int64 v23; // rbx
  __int64 v24; // rdx
  __int64 v25; // rcx
  int v26; // eax
  __int64 v27; // rcx
  __int64 v28; // rax
  __int64 v29; // rcx
  __int64 v30; // rcx
  __int64 v32; // [rsp+28h] [rbp-270h] BYREF
  __int64 v33; // [rsp+30h] [rbp-268h] BYREF
  int v34; // [rsp+38h] [rbp-260h]
  int v35; // [rsp+48h] [rbp-250h]
  char v36[512]; // [rsp+50h] [rbp-248h] BYREF
 
  v32 = a2;
  LOBYTE(a4) = 1;
  if ( (unsigned __int8)sub_1401B70C0(&v32, v36, 256i64, a4) )// if (FParse::Token(Cmd, ClassName, ARRAY_COUNT(ClassName), true))
  {
    v6 = sub_14020CB90(L"/Script/CoreUObject"); // No idea
    v7 = sub_1402766C0(v6, -1i64, v36, 0i64);   // FindObject() since it analyzes v7 in the next if
    if ( v7 )
    {
      v8 = sub_14027A6E0(L"/Script/CoreUObject");// No idea
      LOBYTE(v9) = 1;
      sub_1401FEFE0(&v33, v8, v9, 16i64);       // FObjectIterator
      v10 = v33;
      v11 = v35;
      v12 = v34;
LABEL_4:
      while ( v12 < *(_DWORD *)(v10 + 4112) )   // for loop
      {
        if ( v12 < 0 )
          break;
        v13 = v12 / 0x4000;
        v14 = v12 % 0x4000;
        v15 = *(_QWORD *)(*(_QWORD *)(v10 + 8i64 * (v12 / 0x4000) + 16) + 8 * v14);
        if ( *(_DWORD *)(v15 + 12) > sub_14026F0F0()[1] )// GetUObjectArray()
          break;
        if ( (unsigned int)(*(_DWORD *)(*(_QWORD *)(*(_QWORD *)(*(_QWORD *)(v10 + 8i64 * v13 + 16) + 8 * v14) + 16i64)
                                      + 136i64)
                          - *(_DWORD *)(v7 + 136)) <= *(_DWORD *)(v7 + 140) )
        {
          v16 = *(_QWORD *)(a1 + 64) + 32i64 * (int)sub_140D47260(a1 + 64, 1i64);// AddZeroed()
          v17 = *(_QWORD *)(*(_QWORD *)(v10 + 8i64 * v13 + 16) + 8 * v14);
          *(_DWORD *)(v16 + 24) |= 1u;
          *(_QWORD *)(v16 + 16) = 249i64;
          *(_QWORD *)v16 = v17;
        }
        v18 = *(_DWORD *)(v10 + 4112);
        do
        {
          if ( ++v12 >= v18 )
            break;
          while ( 1 )
          {
            v19 = v12;
            v20 = v12 & 0x3FFF;
            if ( v12 < 0 )
            {
              v19 = v12 + 0x3FFF;
              v20 -= 0x4000;
            }
            if ( *(_QWORD *)(*(_QWORD *)(v10 + 8i64 * (v19 >> 14) + 16) + 8i64 * v20) )
              break;
            if ( ++v12 >= v18 )
              goto LABEL_4;
          }
          v21 = v12;
          v22 = v12 & 0x3FFF;
          if ( v12 < 0 )
          {
            v21 = v12 + 0x3FFF;
            v22 -= 0x4000;
          }
        }
        while ( (v11 & *(_DWORD *)(*(_QWORD *)(*(_QWORD *)(v10 + 8i64 * (v21 >> 14) + 16) + 8i64 * v22) + 8i64)) != 0 );
      }
      v23 = *(int *)(a1 + 72);
      v24 = *(unsigned int *)(a1 + 76);
      v25 = (unsigned int)(v23 + 1);
      *(_DWORD *)(a1 + 72) = v25;
      if ( (int)v25 > (int)v24 )
      {
        v26 = sub_14011BA90(v25, v24, 32i64);   // No idea
        *(_DWORD *)(a1 + 76) = v26;
        v27 = *(_QWORD *)(a1 + 64);
        if ( v27 || v26 )
          *(_QWORD *)(a1 + 64) = sub_140165C50(v27, 32i64 * v26, 0i64);// NO idea
      }
      v28 = *(_QWORD *)(a1 + 64);
      v29 = 32 * v23;
      *(_QWORD *)(v29 + v28) = 0i64;
      *(_QWORD *)(v29 + v28 + 8) = 0i64;
      *(_QWORD *)(v29 + v28 + 16) = 0i64;
      *(_QWORD *)(v29 + v28 + 24) = 0i64;
      v30 = *(_QWORD *)(a1 + 64) + 32 * v23;
      *(_DWORD *)(v30 + 24) |= 1u;
      *(_QWORD *)v30 = v7;
      *(_QWORD *)(v30 + 16) = 249i64;
    }
    else
    {
      sub_1401AA950(a3, L"Object not found");   // Log
    }
  }
  return 1;
}
```

Got into sub_14026F0F0():<br>
<br>

```c++

*sub_14026F0F0()
{
  if ( dword_1421EEF00 <= *(_DWORD *)(*((_QWORD *)NtCurrentTeb()->ThreadLocalStoragePointer + (unsigned int)TlsIndex)
                                    + 16i64) )
    return &dword_1421EDE70;
  Init_thread_header(&dword_1421EEF00);
  if ( dword_1421EEF00 != -1 )
    return &dword_1421EDE70;
  sub_140269280(&dword_1421EDE70);
  atexit(sub_14193BC40);
  Init_thread_footer(&dword_1421EEF00);
  return &dword_1421EDE70;
}
```

It's easy to think that our array could be the returned value: dword_1421EDE70, offset being 21EDE70. UFT gave me 21EDE80. We are there but with this offset of 10, weird, i will try both.<br>
<br>
<b>SIGS &amp;&amp; PDB</b><br>
<br>
Let's open our PDB game and let's see if we have done all correct.<br>
<br>
Well... it seems I got it <img src="https://www.unknowncheats.me/forum/images/smilies/smile.gif" border="0" alt="" title="Big Grin" class="inlineimg"><br>
<br>
	
![Alt 12-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/12.jpg)

<br>
In a YT video a guy said to get the bytes from lea to the call, and that GObject usually starts with 48 8D 0D. <br>
Let's see... well there are a lot that starts with 48 8D 0D and exactly which lea and call should I use? <br>
<br>
I don't know, another question for you.<br>
I admit this is the part where I don't rellay understand what to look.<br>
<br>
Fuck, for the time being I'll take the first i meet.<br>
<br>
Template: 48 8D 0D 30 70 10 02 E8 17 0A 4A 01<br>
Jumper: 48 8D 0D E0 FD F7 01 E8 F7 34 6A 01<br>
Possible sig: 48 8D 0D ?? ?? ?? ?? E8 ?? ?? ?? 01<br>
<br>
</div>
<div id="hide_spoil" style="display: none;">
</div>
</div>
</div></blockquote><br>
<br>
<b>STEP 2: DUMPING GNames &amp;&amp; GObjects</b><br>
<br>
<div style="margin:20px; margin-top:5px">
<div class="smallfont" style="margin-bottom:2px">
<input type="button" value="Hide Spoiler!" style="width:100px;font-size:14px;font-bold:true;margin:10px;padding:0px;" onclick="if (this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display != '') 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = ''; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = 'none'; 
this.value = 'Hide Spoiler!'; 
} 
else 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = 'none'; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = ''; 
this.value = 'Show Spoiler!'; 
}">
<div id="show_spoil" style="margin: 0px; border-style: solid; border-width: 1px; padding: 4px; width: 98%;">
<br>
So we have offsets, will they work? <br>
<br>
Template Game: <br>
GNames: 0x232F530<br>
GObjects: 0x23422C0 or 0x23422B0<br>
<br>
Jumper:<br>
GNames: 0x21DD6B8<br>
GObjects: 0x21EDE80 or 0x21EDE70<br>
<br>
For what I've understood to dump the lists we can use an Instance Logger and inject it in the process.<br>
I've found one here on the forum made by TheFeckless I think.<br>
I have to study this code but I want to see if it works simply changing the offsets.<br>
</div>
<div id="hide_spoil" style="display: none;">
</div>
</div>
</div><br>
<blockquote><br>
<b>STEP 2-a: Dumping JUMPER</b><br>
<br>
<div style="margin:20px; margin-top:5px">
<div class="smallfont" style="margin-bottom:2px">
<input type="button" value="Hide Spoiler!" style="width:100px;font-size:14px;font-bold:true;margin:10px;padding:0px;" onclick="if (this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display != '') 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = ''; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = 'none'; 
this.value = 'Hide Spoiler!'; 
} 
else 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = 'none'; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = ''; 
this.value = 'Show Spoiler!'; 
}">
<div id="show_spoil" style="margin: 0px; border-style: solid; border-width: 1px; padding: 4px; width: 98%;">
<br>
Injected and... <br>
GNames WORKED!<br>
GObjects blank <img src="https://www.unknowncheats.me/forum/images/smilies/sad.gif" border="0" alt="" title="Frown" class="inlineimg"> <br>
I have the other option though.<br>
<br>
Injected and... <br>
GObjects full of INVALID NAME INDEX and shit <img src="https://www.unknowncheats.me/forum/images/smilies/sad.gif" border="0" alt="" title="Frown" class="inlineimg"><br>
<br>
Uff... 2 things may be wrong: <br>
- the offsets -duh<br>
- I need to change something inside the code to match my UE version structure<br>
<br>
I'll start studying the logger code.<br>
</div>
<div id="hide_spoil" style="display: none;">
</div>
</div>
</div><br>
<br>
<b>STEP 2-b: Dumping JUMPER - Why GObjects do not works? - Update 11/01</b><br>
<br>
<div style="margin:20px; margin-top:5px">
<div class="smallfont" style="margin-bottom:2px">
<input type="button" value="Hide Spoiler!" style="width:100px;font-size:14px;font-bold:true;margin:10px;padding:0px;" onclick="if (this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display != '') 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = ''; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = 'none'; 
this.value = 'Hide Spoiler!'; 
} 
else 
{ 
this.parentNode.parentNode.getElementsByTagName('div')['show_spoil'].style.display = 'none'; 
this.parentNode.parentNode.getElementsByTagName('div')['hide_spoil'].style.display = ''; 
this.value = 'Show Spoiler!'; 
}">
<div id="show_spoil" style="margin: 0px; border-style: solid; border-width: 1px; padding: 4px; width: 98%;">
<br>
So... my post is up from a few days now, and no one has yet answered <img src="https://www.unknowncheats.me/forum/images/smilies/cussing.gif" border="0" alt="" title="Cussing" class="inlineimg"><br>
What? You don't like me? Well, I will do it on my own <img src="https://www.unknowncheats.me/forum/images/smilies/fing26.gif" border="0" alt="" title="Fing26" class="inlineimg"><br>
<br>
Jokes aside, let's begin from where we were.<br>
We need to check why GObject is not dumping, we need to check if the offset is good and if the code of the logger need some adjustments.<br>
<br>
<b>Checking the offsets - GNAMES</b><br>
<br>
Let's understand first what we need:<br>
GNames is an array of pointers to names, GNames worked in the dump, so it is good. But let's check it just to understand better.<br>
The offset is 0x21DD6B8, let's open ReClass and check.<br>
<br>
	
![Alt 13-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/13.jpg)

<br>
Ok so we can clearly see there are 2 pointers, let's dereference those and see what they are.<br>
<br>

![Alt 14-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/14.jpg)

<br>
Ok so the first pointer points to other 2 pointers. The second one seems nothing we can use. Let's delete it.<br>
Let's dereference these other 2 pointers we had from the first one.<br>
<br>

![Alt 15-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/15.jpg)

<br>
Ohh, THAT seems an array. Or better, they seems 2 arrays.<br>
Let's see what they are pointing, I will open the first 2 pointers of every array for comparison.<br>
<br>

![Alt 16-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/16.jpg)

<br>
Ok we can see a pattern. Every pointer points to an empty region of the size of 0x10. At 0x10 there is our name.<br>
Like we can see, the first one at offset 0x10 has None. The second has ByteProperty. The first of the second array has MessageIndex. The latter has MessageType.<br>
<br>
Like I expected GNames is good. And since we are here let's put some types and names in this reclass section so we can understand better the structure of 4.10<br>
<br>
So let's see in the source what we are looking, we start like always from the GetNames() method.<br>
<br>

```c++
TNameEntryArray& FName::GetNames()
{
	static TNameEntryArray*	Names = NULL;
	if( Names == NULL )
	{
		check(IsInGameThread());
		Names = new TNameEntryArray();
	}
	return *Names;
}
```

So GetNames() returns a TNameEntryArray, let'go to his definition:<br>
<br>

```c++
typedef TStaticIndirectArrayThreadSafeRead<FNameEntry, 2 * 1024 * 1024 /* 2M unique FNames */, 16384 /* allocated in 64K/128K chunks */ > TNameEntryArray;
```

Woo, and what is that? Definition of TStaticIndirectArrayThreadSafeRead:<br>
<br>

```c++
/**
 * Simple array type that can be expanded without invalidating existing entries.
 * This is critical to thread safe FNames.
 *    @Param ElementType Type of the pointer we are storing in the array
 *    @Param MaxTotalElements absolute maximum number of elements this array can ever hold
 *    @Param ElementsPerChunk how many elements to allocate in a chunk
 **/
 template<typename ElementType, int32 MaxTotalElements, int32 ElementsPerChunk>
class TStaticIndirectArrayThreadSafeRead
{
	enum
	{
		// figure out how many elements we need in the master table
		ChunkTableSize = (MaxTotalElements + ElementsPerChunk - 1) / ElementsPerChunk
	};
	/** Static master table to chunks of pointers **/
	ElementType** Chunks[ChunkTableSize];
	/** Number of elements we currently have **/
	int32 NumElements;
	/** Number of chunks we currently have **/
	int32 NumChunks;
```

Ok so is basically a standard array, the first parameter is the type of data it's holding and the others parameters define how this array is divided in multiple chunks.<br>
So going back at the definition of TNameEntryArray: it is an array that contains FNameEntry.<br>
<br>
Definition of FNameEntry:<br>
<br>

```c++

/**
 * A global name, as stored in the global name table.
 */
struct FNameEntry
{
private:
	/** Index of name in hash. */
	NAME_INDEX		Index;
 
public:
	/** Pointer to the next entry in this hash bin's linked list. */
	FNameEntry*		HashNext;
 
private:
	/** Name, variable-sized - note that AllocateNameEntry only allocates memory as needed. */
	union
	{
		ANSICHAR	AnsiName[NAME_SIZE];
		WIDECHAR	WideName[NAME_SIZE];
	};
```

Here we are! So AnsiName is probably our name (None ecc), FNameEntry is a pointer, Index is an int32, but we avance some space if math isn't an opinion. The name was at offset 0x10 so there is probably some extra space between HashNext and the name. <br>
Let's put all of this in ReClass:<br>
<br>

![Alt 17-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/17.jpg)

<br>
Ok so basically we understand 2 things, indexes goes by 2, because... yes.<br>
We see 2 arrays, and the first element of the second has index 32768. 32768/2 = 16384! The number we've seen in the definition! All make sense.<br>
<br>
So we can go backwards and name everything else in ReClass.<br>
<br>
At the and we have a structure like this:<br>
<br>
- Our offset points to all the arrays with names in it<br>
<br>

![Alt 18-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/18.jpg)

<br>
- Those pointers refers to the vary entries of those arrays:<br>
<br>

![Alt 19-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/19.jpg)

<br>
Simple like drinking a glass of water, like we say here.<br>
<br>
<b>Checking the offsets - GOBJECTS</b><br>
<br>
So now.. our enemy.<br>
<br>
We start with 2 offsets but they are very close, let's put the smaller one so we can see even the other in ReClass.<br>
0x21EDE70 or 0x21EDE80<br>
<br>

![Alt 20-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/20.jpg)

<br>
Ok the pointers are at 0x..80 so the one I picked from IDA was wrong. But come on, so close, UFT gave me the 80 one but I am confident that even without it I would have it spotted.<br>
<br>
Let's dereference those:<br>
<br>

![Alt 21-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/21.jpg)

<br>
Ok it seems we have already two arrays, seems very similar to the GNames structure. Let's open the first two of every array:<br>
<br>

![Alt 22-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/22.jpg)

<br>
Oh we are of course watching to an array of similar objects. On the internet I've seen what an UObject should look like, and the only thing clearly equal to those I've seen on the web is the first pointer: that should be a VTable.<br>
Now let's look at the source and let's see if we can understand the structure.<br>
<br>
Start from GetUObjectArray():<br>
<br>

```c++
FUObjectArray& GetUObjectArray()
{
	static FUObjectArray GlobalUObjectArray;
	return GlobalUObjectArray;
}
```

Returns an FUObjectArray:<br>
<br>

```c++
	/** First index into objects array taken into account for GC.							*/
	int32 ObjFirstGCIndex;
	/** Index pointing to last object created in range disregarded for GC.					*/
	int32 ObjLastNonGCIndex;
	/** If true this is the intial load and we should load objects int the disregarded for GC range.	*/
	int32 OpenForDisregardForGC;
	/** Array of all live objects.											*/
	TUObjectArray ObjObjects;
```

Ok so another array apparently: TUObjectArray <br>
<br>

```c++
typedef TStaticIndirectArrayThreadSafeRead<UObjectBase, 8 * 1024 * 1024 /* Max 8M UObjects */, 16384 /* allocated in 64K/128K chunks */ > TUObjectArray;
```

Oh, just like the array of the names, remember? This one is made of UObjectBase though:<br>
<br>

```c++
	/** Flags used to track and report various object states. This needs to be 8 byte aligned on 32-bit
	    platforms to reduce memory waste */
	EObjectFlags					ObjectFlags;
 
	/** Index into GObjectArray...very private. */
	int32								InternalIndex;
 
	/** Class the object belongs to. */
	UClass*							Class;
 
	/** Name of this object */
	FName							Name;
 
	/** Object this object resides in. */
	UObject*						Outer;
```

Here we are: this should be our UObject, let's take a look at FName:<br>
<br>

```c++
	/** Index into the Names array (used to find String portion of the string/number pair used for comparison) */
	NAME_INDEX		ComparisonIndex;
#if WITH_CASE_PRESERVING_NAME
	/** Index into the Names array (used to find String portion of the string/number pair used for display) */
	NAME_INDEX		DisplayIndex;
#endif
	/** Number portion of the string/number pair (stored internally as 1 more than actual, so zero'd memory will be the default, no-instance case) */
	uint32			Number;
```

Ok so basically FName has an index (int32). This integer refer to the GName array, and here's why we need both.<br>
For every object we take, we see that index, search that index in the Name array and we have the name of the object!<br>
All clear, let's try to put that in ReClass and if matches:<br>
<br>

![Alt 23-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/23.jpg)

<br>
This seems pretty good to me, InternalIndex grows by one this time (0, 1 - 16384, 16385), 16384 is the first of the second chunk: 16384 / 1 = 16384 (remeber the definition of TUObjectArray?) and we see the FName Index, apparently the first one has Index 688, and in my dump of GNames that is CoreUObject.<br>
<br>
Ok so let's go backwards and define all.<br>
<br>

![Alt 24-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/24.jpg)

<br>
2 things: <br>
- this structure is one pointer shorter than GNames like we can see, basically it's like what I've called here GObject is at the same level of what I've called PtrToAllNameEntryArray in the GNames ReClass.<br>
- We don't need to go up to FUObjectArray and define that, our pointer points directly to TUObjectArray, so why bother?<br>
<br>
Offsets good apparently, time to check the InstanceLogger code!<br>
<br>
<b>Checking the InstanceLogger code</b><br>
<br>
Like I've said, I've found it here on the forum.<br>
First things firts, if you have compiling problem add #include &lt;Psapi.h&gt;, I needed it in VS2019.<br>
<br>
I'd like to go by order so let'start from DllMain:<br>
<br>

```c++
BOOL WINAPI DllMain(HMODULE hModule, DWORD dwReason, LPVOID lpReserved)
{
    switch (dwReason)
    {
    case DLL_PROCESS_ATTACH:
        DisableThreadLibraryCalls(hModule);
        CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)onAttach, NULL, 0, NULL);
        return true;
        break;
 
    case DLL_PROCESS_DETACH:
        return true;
        break;
    }
}
```

Very basic, let's see onAttach() then:<br>
<br>

```c++
void onAttach()
{
    AllocConsole();
    freopen("CONOUT$", "w", stdout);
 
    MODULEINFO miGame = GetModuleInfo(NULL);
 
    GObjObjects_offset = (DWORD64)((DWORD64)miGame.lpBaseOfDll + 0x21EDE80);
    Names_offset = (*(DWORD64*)((DWORD64)miGame.lpBaseOfDll + 0x21DD6B8));
 
    GObjObjects = (FUObjectArray*)GObjObjects_offset;
    Names = (TNameEntryArray*)Names_offset;
 
    NameDump();
    ObjectDump();
}
```

Ok, now Names works, so let' see what it's doing, it takes the offset and it dereference it so the program wants the pointer to the first chunk, this one for understand:<br>
<br>

![Alt 25-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/25.jpg)

<br>
Well the GObject offset we are giving points already to the same location but for the objects so no need to dereference: <br>
<br>

```c++
    GObjObjects_offset = ((DWORD64)miGame.lpBaseOfDll + 0x21EDE80);
    Names_offset = (*(DWORD64*)((DWORD64)miGame.lpBaseOfDll + 0x21DD6B8));
```

Then next couple of lines, Names is good, GObjObjects no... don't need FUObjectArray, let's fix it:<br>
<br>

```c++
    GObjObjects = (TUObjectArray*)GObjObjects_offset;
    Names = (TNameEntryArray*)Names_offset;
```

Now the definitions:<br>
<br>

```c++
using TNameEntryArray = TStaticIndirectArrayThreadSafeRead<FNameEntry, 2 * 1024 * 1024, 16384>;
```

Oh just like the source, FNameEntry and TStaticIndirectArrayThreadSafeRead:<br>
<br>

```c++
struct FNameEntry
{
    int Index;
    char pad_0x0004[0x4];
    FNameEntry* HashNext;
    char AnsiName[1024];
};
```

See the padding, I'm not a complete idiot come on.<br>
<br>

```c++
template<typename ElementType, __int32 MaxTotalElements, __int32 ElementsPerChunk>
class TStaticIndirectArrayThreadSafeRead
{
public:
    __int32 Num() const
    {
        return numElements;
    }
 
    bool IsValidIndex(__int32 index) const
    {
        return index >= 0 && index < Num() && GetById(index) != nullptr;
    }
 
    ElementType const* const& GetById(__int32 index) const
    {
        return *GetItemPtr(index);
    }
 
private:
    ElementType const* const* GetItemPtr(__int32 Index) const
    {
        const __int32 ChunkIndex = Index / ElementsPerChunk;
        const __int32 WithinChunkIndex = Index % ElementsPerChunk;
        const auto Chunk = chunks[ChunkIndex];
        return Chunk + WithinChunkIndex;
    }
 
    enum
    {
        ChunkTableSize = (MaxTotalElements + ElementsPerChunk - 1) / ElementsPerChunk
    };
 
    ElementType** chunks[ChunkTableSize];
    __int32 numElements;
    __int32 numChunks;
};
```

That's f*cking perfect! Need to hug this man, make sense that GNames works.<br>
Let's see TUObjectArray though:<br>
<br>

```c++
class TUObjectArray
{
public:
    FUObjectItem* Objects;
    __int32 MaxElements;
    __int32 NumElements;
};
```

Mmm... nope, that's clearly a different structure, our TObjectArray should be like this, let's edit it:<br>
<br>

```c++
using TUObjectArray = TStaticIndirectArrayThreadSafeRead<UObjectBase, 8 * 1024 * 1024, 16384>;
```

Ok let'see if there is UObjectBase in the logger... nope, but there is UObject, should be similar, let's see:<br>
<br>

```c++
struct UObject
{
    UCHAR   Unknown[0x10];       // unknowed data
    DWORD   NameIndex;                              // struct FName
};
```

Yeah so apparently it wants only to know where is the index of FName, make sense, in our case so we can change it in:<br>
<br>

```c++
struct UObjectBase
{
    UCHAR   Unknown[0x18];       // unknowed data
    DWORD   NameIndex;                              // struct FName
};
```

0x18, go see the ReClass images.<br>
<br>
Ok then it calls the Dump methods<br>
<br>

```c++
void ObjectDump()
{
    FILE* Log = NULL;
    fopen_s(&Log, "ObjectDump.txt", "w+");
 
    for (DWORD64 i = 0x0; i < GObjObjects->ObjObjects.NumElements; i++)
    {
        if (!GObjObjects->ObjObjects.Objects[i].Object) { continue; }
 
        fprintf(Log, "UObject[%06i] %-50s 0x%llX\n", i, GetName(GObjObjects->ObjObjects.Objects[i].Object), GObjObjects->ObjObjects.Objects[i].Object);
    }
 
    fclose(Log);
}
 
void NameDump()
{
    FILE* Log = NULL;
    fopen_s(&Log, "NameDump.txt", "w+");
 
    for (DWORD64 i = 0x0; i < Names->Num(); i++)
    {
        if (!Names->GetById(i)) { continue; }
 
        fprintf(Log, "Name[%06i] %s\n", i, Names->GetById(i)->AnsiName);
    }
 
    fclose(Log);
}
```

Ok so we can clearly see how the entire structure of GObject is different, in this case the program take in account FUObject, look inside for TUObject, goes to FUObjectItem and then takes the UObject:<br>
<br>

```c++
struct UObject
{
    UCHAR   Unknown[0x10];       // unknowed data
    DWORD   NameIndex;                              // struct FName
};
 
class FUObjectItem
{
public:
    UObject* Object;
    __int32 Flags;
    __int32 ClusterIndex;
    __int32 SerialNumber;
    char unknowndata_00[0x4]; //New
};
 
class TUObjectArray
{
public:
    FUObjectItem* Objects;
    __int32 MaxElements;
    __int32 NumElements;
};
 
class FUObjectArray
{
public:
    __int32 ObjFirstGCIndex; //0x0000
    __int32 ObjLastNonGCIndex; //0x0004
    __int32 MaxObjectsNotConsideredByGC; //0x0008
    __int32 OpenForDisregardForGC; //0x000C
 
    TUObjectArray ObjObjects;
};
```

We don't need any of that, just comment it out.<br>
Then we can change the ObjectDump method to suits us:<br>
<br>

```c++
void ObjectDump()
{
    FILE* Log = NULL;
    fopen_s(&Log, "ObjectDump.txt", "w+");
 
    //for (DWORD64 i = 0x0; i < GObjObjects->ObjObjects.NumElements; i++)
    for (DWORD64 i = 0x0; i < GObjObjects->Num(); i++)
    {
        //if (!GObjObjects->ObjObjects.Objects[i].Object) { continue; }
        if (!GObjObjects->GetById(i)) { continue; }
 
        //fprintf(Log, "UObject[%06i] %-50s 0x%llX\n", i, GetName(GObjObjects->ObjObjects.Objects[i].Object), GObjObjects->ObjObjects.Objects[i].Object);
        fprintf(Log, "UObject[%06i] %-50s 0x%p\n", i, GetName(GObjObjects->GetById(i)), GObjObjects->GetById(i));
    }
 
    fclose(Log);
}
```

NameDump() iterates the array, and for every member prints the index then goes into the AnsiName variable ant prints it into the file.<br>
<br>
ObjectDump() iterates the array, and for every member prints the index, prints the return value of GetName() and prints the address of the Object.<br>
<br>
Ok only GetName() remains:<br>
<br>

```c++
char* GetName(UObject* Object)
{
    DWORD64 NameIndex = *(PDWORD64)((DWORD64)Object + Offset_Name);
 
    if (NameIndex < 0 || NameIndex > Names->Num())
    {
        static char ret[256];
        sprintf_s(ret, "INVALID NAME INDEX : %i > %i", NameIndex, Names->Num());
        return ret;
    }
    else
    {
        return (char*)Names->GetById(NameIndex)->AnsiName;
    }
}
```

Ok for start, the first line is complicated for nothing here, it want to understand where is the offset of the FName index<br>
Well... just:<br>
<br>

```c++
int NameIndex = Object->NameIndex;
```

All the rest seems good, it take the FName Index of the object and it goes to see what matches in the Names array.<br>
<br>
GetModuleInfo, bDataCompare and FindPattern are for sigs, I haven't even looked at them, I hate sigs, I don't understand them. <img src="https://www.unknowncheats.me/forum/images/smilies/angry.gif" border="0" alt="" title="angry" class="inlineimg"><br>
<br>
Ok so our modified version should look like this:<br>
<br>

```c++
#include <Windows.h>
#include <stdio.h>
#include <Psapi.h>
#include <cstring>
#include <iostream>
 
DWORD64   GObjObjects_offset = NULL;
DWORD64   Names_offset = NULL;
 
emplate<typename ElementType, __int32 MaxTotalElements, __int32 ElementsPerChunk>
class TStaticIndirectArrayThreadSafeRead
{
public:
    __int32 Num() const
    {
        return numElements;
    }
 
    bool IsValidIndex(__int32 index) const
    {
        return index >= 0 && index < Num() && GetById(index) != nullptr;
    }
 
    ElementType const* const& GetById(__int32 index) const
    {
        if (doonce) std::cout << "*GetItemPtr(index): " << *GetItemPtr(index) << " GetItemPtr(index): " << GetItemPtr(index) <<  std::endl;
        doonce = false;
        return *GetItemPtr(index);
    }
 
private:
    ElementType const* const* GetItemPtr(__int32 Index) const
    {
        const __int32 ChunkIndex = Index / ElementsPerChunk;
        const __int32 WithinChunkIndex = Index % ElementsPerChunk;
        const auto Chunk = chunks[ChunkIndex];
        if (doonce2) std::cout << "Chunk: " << Chunk << " chunks[ChunkIndex]: " << chunks[ChunkIndex] << " Chunk + WithinChunkIndex: " << Chunk + WithinChunkIndex << std::endl;
        doonce2 = false;
        return Chunk + WithinChunkIndex;
    }
 
    enum
    {
        ChunkTableSize = (MaxTotalElements + ElementsPerChunk - 1) / ElementsPerChunk
    };
 
    ElementType** chunks[ChunkTableSize];
    __int32 numElements;
    __int32 numChunks;
};
 
struct UObjectBase
{
    UCHAR   Unknown[0x18];       // unknowed data
    DWORD   NameIndex;                              // struct FName
};
 
using TUObjectArray = TStaticIndirectArrayThreadSafeRead<UObjectBase, 8 * 1024 * 1024, 16384>;
 
struct FNameEntry
{
    int Index;
    char pad_0x0004[0x4];
    FNameEntry* HashNext;
    char AnsiName[1024];
};
 
using TNameEntryArray = TStaticIndirectArrayThreadSafeRead<FNameEntry, 2 * 1024 * 1024, 16384>;
 
TUObjectArray* GObjObjects = NULL;
TNameEntryArray* Names = NULL;
 
char* GetName(const UObjectBase* Object)
{
    int NameIndex = Object->NameIndex;
 
    std::cout << NameIndex << std::endl;
 
    if (NameIndex < 0 || NameIndex > Names->Num())
    {
        static char ret[256];
        sprintf_s(ret, "INVALID NAME INDEX : %i > %i", NameIndex, Names->Num());
        return ret;
    }
    else
    {
        return (char*)Names->GetById(NameIndex)->AnsiName;
    }
}
 
void ObjectDump()
{
    FILE* Log = NULL;
    fopen_s(&Log, "ObjectDump.txt", "w+");
 
    for (DWORD64 i = 0x0; i < GObjObjects->Num(); i++)
    {
        if (!GObjObjects->GetById(i)) { continue; }
 
        fprintf(Log, "UObject[%06i] %-50s 0x%p\n", i, GetName(GObjObjects->GetById(i)), GObjObjects->GetById(i));
    }
 
    fclose(Log);
}
 
void NameDump()
{
    FILE* Log = NULL;
    fopen_s(&Log, "NameDump.txt", "w+");
 
    for (DWORD64 i = 0x0; i < Names->Num(); i++)
    {
        if (!Names->GetById(i)) { continue; }
 
        fprintf(Log, "Name[%06i] %s\n ", i, Names->GetById(i)->AnsiName);
    }
 
    fclose(Log);
}
 
void onAttach()
{
    AllocConsole();
    freopen("CONOUT$", "w", stdout);
 
    MODULEINFO miGame = GetModuleInfo(NULL);
 
    GObjObjects_offset = ((DWORD64)miGame.lpBaseOfDll + 0x21EDE80);
    Names_offset = (*(DWORD64*)((DWORD64)miGame.lpBaseOfDll + 0x21DD6B8));
 
    GObjObjects = (TUObjectArray*)GObjObjects_offset;
    Names = (TNameEntryArray*)Names_offset;
 
    NameDump();
    ObjectDump();
}
 
BOOL WINAPI DllMain(HMODULE hModule, DWORD dwReason, LPVOID lpReserved)
{
    switch (dwReason)
    {
    case DLL_PROCESS_ATTACH:
        DisableThreadLibraryCalls(hModule);
        CreateThread(NULL, 0, (LPTHREAD_START_ROUTINE)onAttach, NULL, 0, NULL);
        return true;
        break;
 
    case DLL_PROCESS_DETACH:
        return true;
        break;
    }
}
```

BUILD TIME!<br>
<br>
and...<br>
<br>
<img src="https://www.unknowncheats.me/forum/images/smilies/cool.gif" border="0" alt="" title="Cool" class="inlineimg"> IT WORKS <img src="https://www.unknowncheats.me/forum/images/smilies/cool.gif" border="0" alt="" title="Cool" class="inlineimg"><br>
<br>

![Alt 26-png](https://raw.githubusercontent.com/untyper/UE4.1x_Journey/main/img/26.jpg)

<br>
Wow I wasn't expect it, uhm ok.<br>
<br>
So now from what I understand I have to make an SDK. And there is a Generator from KN4CK3R out there.<br>
More code-study time!<br>
</div>
<div id="hide_spoil" style="display: none;">
</div>
</div>
</div><br>
<br>
</blockquote></div>
<div id="hide_spoil">
</div>
</div>
</div><br>
<br>
<b>QUESTIONS</b><br>
<br>
- [Read end of 1.b and start of 1.c for more info] Why in the function I picked to find GetNames() (sub_1401BD5C0, FName::InitInternal_FindOrAddNameEntry()) i wasn't able to find it? I was expecting to find a sub_xxxx (GetNames()) and inside it find the offset of the array I needed. But instead I've found directly the offset in FindOrAddNameEntry(). Little bad of course, but why?<br>
<br>
- [Read section SIGS &amp;&amp; PDB in 1.c for more info] What instruction interest to me when I want to grab the sigs for GNames or GObjects? I'm taking offsets to the arrays in IDA, but when i have to do with sigs I don't understand what I need to look.<br>
<br>
- Of course if you want to give me advices or correct anything I had said wrong, and there are probably a lot of things , I will be very pleased.<br>
<br>
<br>
-----------------------------------------------------------------------------------------------------<br>
Hope to have not violated any of the rules, I want of course to update this journey as I go forward, everytime I will make a step, I will update the post.<br>
<br>
Thanks for the reading, <br>
<br>
Cafo.</div>
