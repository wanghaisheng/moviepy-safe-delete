# moviepy-safe-delete

if you are confusing by permission error try to delete tmp video files but got permission error,try this


    if len(freemusic) > 0:    
        soundeffect = random.choice(freemusic)
        print('randomly choose a background music',soundeffect)
        ext = os.path.splitext(soundeffect)[1]
        videoext= os.path.splitext(inputmp4)[1]
        videofilename= os.path.splitext(inputmp4)[0]

        print('videoext',videoext)
        print('videofilename',videofilename)
        oldvideofiles=[]

        audioclip = AudioFileClip(soundeffect)
        if not os.path.exists(videofilename+'-old'+videoext):
            os.rename(inputmp4, videofilename+'-old'+videoext)
        videoclip = VideoFileClip(videofilename+'-old'+videoext)
        if audioclip.duration>videoclip.duration:
            audioclip =audioclip.subclip(0,videoclip.duration)
        else:
            audioclip = vfx.loop( audioclip, duration=videoclip.duration)
        if setting['ratio']:
            pass
        else:
            setting['ratio']=1
        # audioclip = audioclip.fx( afx.volumex, float(setting['ratio']))
        # audioclip.write_audiofile(videofilename+'.mp3')

        # audioclip = volumex(audioclip,setting['ratio'])          
        videoclip = videoclip.set_audio(audioclip)

        videoclip.write_videofile(videofilename+'.mp4', threads=0, audio=True)
        if not videoclip == None:
            print('force close clip')
            audioclip.close()

            videoclip.close()

            del audioclip 
            del videoclip 
 
            import gc 
            gc.collect()

                   print('start cleaning old video file')
        if os.path.exists(videofilename+'-old'+videoext):
            os.remove(videofilename+'-old'+videoext)
