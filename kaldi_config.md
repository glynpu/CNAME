以 compute-vad为例，其能接受--config 参数是因为  
ParseOptions 类(OptionsItf的子类)的[Read](https://github.com/kaldi-asr/kaldi/blob/df1ebbc9fdc7e466ac9b318baa4215f68aa60db0/src/ivectorbin/compute-vad.cc#L51)函数为[试图读取](https://github.com/kaldi-asr/kaldi/blob/8ce3a95761e0eb97d95d3db2fcb6b2bfb7ffec5b/src/util/parse-options.cc#L346)config 文件  
为什么读取config 文件后，会修改 VadEnergyOptions 中各成员变量的值？
VadEnergyOptions结构体中的[Register函数](https://github.com/kaldi-asr/kaldi/blob/155c65894d1405fb99c2abb7858ad8b0748a82d5/src/ivector/voice-activity-detection.h#L52)为将其各成员变量与ParseOptoins中的[map 绑定起来](https://github.com/kaldi-asr/kaldi/blob/8ce3a95761e0eb97d95d3db2fcb6b2bfb7ffec5b/src/util/parse-options.cc#L102)  

ParseOptions 的[ReadConfigFile函数](https://github.com/kaldi-asr/kaldi/blob/8ce3a95761e0eb97d95d3db2fcb6b2bfb7ffec5b/src/util/parse-options.cc#L466)会由map表存放的指针修改 VadEnergyOptions 中各成员变量的值


config 文件中各种类型的参数需要转换成float/intager之类的，转换函数在如[ConvertStringToInteger](https://github.com/kaldi-asr/kaldi/blob/155c65894d1405fb99c2abb7858ad8b0748a82d5/src/util/text-utils.h#L118) 定义在 [util/text-utils.h](https://github.com/kaldi-asr/kaldi/blob/master/src/util/text-utils.h)
 
  

