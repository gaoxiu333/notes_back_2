

## 基本命令


**play**: 播放音符或频率。
 
```rubyÏ
play 60  # 播放 MIDI 音符号 60
```

**sleep**: 暂停一定时间。

```ruby
sleep 1  # 暂停 1 秒
```

**sample**: 播放样本音频。
 
```ruby
sample :drum_heavy_kick  # 播放重型踢鼓样本
```

**use_bpm**: 设置曲速（每分钟的拍数）。

```ruby
use_bpm 120  # 设置速度为 120 拍每分钟
```

**in_thread**: 创建新线程以并行运行代码块。   
 
```ruby
in_thread do
  play 60
end

in_thread do
  sample :drum_snare_hard
end

```

循环

```ruby
# 无限循环
loop do 
	play 60 
	sleep 1 
end
# 指定循环次数
8.times do 
	play 60 
	sleep 0.5 
end
```


## 合成器

用来合成或者创造声音，原理是通过振荡器，滤波器灯来控制声音。

选项或者参数

```ruby
# 振幅器 - 放大音量 | 0 ～ ∞
play 60, amp: 0.5

# 平移 - 控制左右声道 ｜ -1 左声道，1右声道，0 两者中心
paly 60, pan: 1

```

使用合成器

```ruby
use_synth :saw
```


控制声音

```ruby
# 释放 - release ｜  0 ～ ∞ （单位s）
# 起音 - attack
# 持续 - sustain
play 60, attack: 0.1, attack_level: 1, decay: 0.2, sustain_level: 0.4, sustain: 1, release: 0.5
```

![[Pasted image 20231223210546.png]]
淡入淡出效果

```ruby
sample :loop_amen, attack: 0.75, release: 0.75
```


## 样本

提前录制好的声音

```ruby
# 播放样本
sample :ambi_drone
```

**rate**

拉伸压缩声音

```ruby
# 降低声音，并且将播放时长增加两倍 ｜ 0 ～ ∞ ｜ 可以是负数
sample :ambi_choir, rate:0.5
```

指定起点和终点

```ruby
sample :loop_amen, start: 0.4, finish: 0.6
```

