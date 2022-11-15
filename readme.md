# MainBoard 1.59 使用说明
*Version：0.0.2*</br>
*Last Update: 2022/11/14*</br>
*Update:
2022/11/14  补充MP3模块、电机驱动模块、继电器驱动模块代码及说明
2022/11/12  优化排版，完善表格显示
2022/11/10  创建文档*</br>
## 接口说明
+ ![左侧](IMG_20221110_225504.jpg)
   + 中间是[**Arduino Nano V3**](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=546856450454&_u=a2e8a0g13a95)自带的Mini-usb，用于程序下载及查看串口日志。也可用于轻负载(对用电需求不高)场景下的调试。
   + 底部绿色[拔插式接线端子](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=544387195069&_u=a2e8a0g14021)为12V供电输入。**注意：此处靠近Arduino一侧为+12V，另一侧为0V***（下一版会放到正面，但供电方向不变，都是以靠近Arduino一侧为正）*
   + 最右侧为DC 5.5电源插座，方便12V电源供电。（供电接一处即可）
+ ![背侧](IMG_20221110_225515.jpg)
   + 左侧为[TB6612](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=616029257488&_u=a2e8a0g13bfb)电机接口，但因价格较贵预计下一版取消。
   + 中间为绿色[**双层**拔插式接线端子](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=640795760513&_u=a2e8a0g1e2df)，可直接磁锁或其他12V/5V灯等设备。
   + 右侧为[黄色跳线帽](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=15486563850&_u=a2e8a0g13761)，用于切换双层接线端子输出电压（12V/5V）。
+ ![右侧](IMG_20221110_225529.jpg)
   + 左侧为[继电器*5脚SRD-5V*](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=178521653&_u=b2e8a0g1f928)输出，其中NO为常开端，COM为公共端，NC为常闭端
   + **第二个继电器与电机驱动存在干涉，无法共同使用**。下一版可能修复，也可去掉一个铜柱，以牺牲电机驱动（L298N）稳定性强行使用。
   + 中间[按钮](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=557056221871&_u=b2e8a0g13fc2) (*被挡住了*)为Arduino复位按钮，直连Arduino的RST引脚
   + 按钮右边是电机驱动模块[(L298N)](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=16548618931&_u=b2e8a0g18c52)的供电接口，朝向相同时线序相同。但不同模块供应商可能存在差异，从左到右依次为+12V，GND，+5V。
   + 最右是[DFPlayer MP3播放模块](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=530156137867&_u=b2e8a0g1f89c)，其下方为TRS耳机接口。</br>**TRS指3线耳机接线，与TRRS即包含麦克风的四线插头不兼容**</br>模块含TF卡槽，支持MP3、WAV、WMA等格式，FAT16、FAT32文件系统，文件需以0001-0999序号命名。
+ ![前侧](IMG_20221110_225541.jpg)
   + MP3模块背后为5V和12V[电源端子*2P直针座*](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=544387195069&_u=b2e8a0g1e0ba)，输入/输出均可
   + [RJ45网线接口*2x4无灯无弹*](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=575521582267&_u=b2e8a0g1f062)
   + 以从左到右，从上到下的顺序命名为Port1-Port8。接口统一，1线为+5V，8线为GND，其余按照线序排列，若无则为空。
   + Port1：SPI接口，适用于[Nokia 5110显示屏](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=527625958802&_u=b2e8a0g19752)、[MFRC-522 RFID](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=557141693021&_u=b2e8a0g17c09)等模块
   + Port2: 双线接口，适用于[超声波](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=586186408547&_u=b2e8a0g18b56)、[麦克风](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=532756660832&_u=b2e8a0g1649f)等传感器，可用于模拟信号输入（即判断声音等信号大小）。也可用作软件串口。
   + Port3、Port4：单线接口，适用于麦克风、光线、震动等传感器，只能识别是否触发。
   + Port5 ~ Port7：IIC接口，适用于[0.96寸显示屏](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=575274211818&_u=b2e8a0g1dfb8)等一系列以IIC为通讯协议的外部设备
   + Port8：硬件串行接口，适用于[433MHz无线传输](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=20265137304&_u=b2e8a0g12491)等一系列以UART为通讯协议的外部设备
## 模块使用说明
### 电源降压模块
 + [MP1584EN](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=534989436855&_u=b2e8a0g1cb1a)
 12V转5V，最大电流为3A（**不可持续**）<br/>
 + [0.25A保险丝](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=561597058073&_u=b2e8a0g1061f)
 保护Arduino Nano，电源端子和双层端子不受该电流限制
### DFPlayer MP3模块
 + 通过软串口与Arduino连接 RX -> A1; TX -> A0
 + Arduino库 -> [DFRobotDFPlayerMini](https://github.com/DFRobot/DFRobotDFPlayerMini)
 + 模块含TF卡槽，支持MP3、WAV、WMA等格式，FAT16、FAT32文件系统，
 + 文件需以0001-0999序号命名。</br>
 **以下是模块的使用教程**
  1. 首先，点击[DFRobotDFPlayerMini](https://github.com/DFRobot/DFRobotDFPlayerMini)，而后点击页面绿色Code按钮，选择Download Zip下载第三方库。
  2. 打开Arduino IDE *(推荐版本1.8.19)*，依次选择*项目-加载库-添加.ZIP库*，按照下载路径选中压缩文件。
  3. 而后你便可以在*文件-示例-DFRobotDFPlayerMini*中查看自带的示例程序。以下将对其中部分代码作解释说明。
   </br>
```

SoftwareSerial mySoftwareSerial(A0, A1); // RX, TX 定义与模块连接的引脚，在MainBoard1.59上为A0和A1

void setup()
{
   //必须存在的函数，该函数内代码仅会在开机时运行一次，而后除非重启不再运行

   Serial.begin(9600);//该句为Arduino与电脑通信的基础，方便我们判断程序状态

   //以下为MP3模块配置代码，必须
   mySoftwareSerial.begin(9600); //定义传输速率，不可更改
   if (!myDFPlayer.begin(mySoftwareSerial)) {  //该句用于判断Arduino是否已能与模块正常通信
   //即当myDFPlayer.begin(mySoftwareSerial)=0 时出错
   //若出错，首先应检查模块连接是否完好，焊接是否存在缺焊虚焊
   //其次检查首行代码，其连接是否与板子背面标注一致，尝试更换二者位置
   //每次更改后请重新上传程序至Arduino （快捷键Ctrl+U）
      Serial.println("MP3模块连接错误，请检查");//可通过Arduino IDE中的工具-串口监视器查看提示信息 （快捷键Ctrl+Shift+M）
      while(true){}//死循环，程序在此停止


      myDFPlayer.volume(10);  //若能正常通信，则设定音量，为0~30可调，必须
  }

/////////////////////////////////////////////////////////////////////////////////////////
/////////////////////////////////////////////////////////////////////////////////////////
   //以下为MP3模块功能代码（均为非必须，按照需要调用即可）
   myDFPlayer.play(1);  //播放文件名为0001，格式为mp3/wav/wma的音效，播完暂停。根据需要更改参数。

   myDFPlayer.previous();  //Play previous mp3 播放上一首，非必须

   myDFPlayer.loop(1);  //Loop the first mp3 循环播放文件名为001，格式为mp3/wav/wma的音效

   myDFPlayer.pause();  //pause the mp3 暂停播放，非必须

   myDFPlayer.start();  //start the mp3 from the pause 继续播放，非必须

   myDFPlayer.enableLoopAll(); //loop all mp3 files. 按文件顺序循环播放所有音效，非必须

   myDFPlayer.disableLoopAll(); //stop loop all mp3 files. 停止循环播放

   myDFPlayer.playFolder(15, 4);  //播放文件夹名为“15”中文件名为004的音效，文件夹名可为1~99，文件名可为1~255

   myDFPlayer.playLargeFolder(2, 999); //为超大文件夹提供支持。播放文件夹名为“02”中文件名为999的音效，文件夹名可为1~10，文件名可为1~1000

   myDFPlayer.playMp3Folder(4); /播放文件夹名为“MP3”中文件名为004的音效，文件名可为0~65535

   myDFPlayer.randomAll(); //Random play all the mp3. 随机播放所有音效

   Serial.println(myDFPlayer.readVolume()); //read current volume 读取当前音量，并传输至电脑。

   Serial.println(myDFPlayer.readFileCounts()); //read all file counts in SD card 读取当前SD卡内文件数量

   Serial.println(myDFPlayer.readCurrentFileNumber()); //read current play file number 读取当前播放的文件名称

   Serial.println(myDFPlayer.readFileCountsInFolder(3)); //read file counts in folder SD:/03 读取当前播放的文件所在的文件夹名称
}

```
### 电机驱动模块 L298N
 + M1与M2可同时控制<br/>
 + 无法通过PWM进行调速（已置高）<br/>

    |电机/推杆|旋转方式|IN1(D2)|IN2(D3)|IN3(D4)|IN4(D5)|
    |:------:|:-----:|:-----:|:------:|:-----:|:----:|
    | M1     | 正转   | 1     | 0     | /     |/     |
    | M1     | 反转   | 0     | 1     | /     |/     |
    | M1     | 停止   | 0     | 0     | /     |/     |
    | M2     | 正转   | /     | /     | 1     |0     |
    | M2     | 反转   | /     | /     | 0     |1     |
    | M2     | 停止   | /     | /     | 0     |0     |
    </br>

```
void setup()
{
//必须存在的函数，该函数内代码仅会在开机时运行一次，而后除非重启不再运行

   Serial.begin(9600);//Serial.begin(9600);//该句为Arduino与电脑通信的基础，方便我们判断程序状态


   for (int i=2;i<=5;i++){
      pinMode(i,OUTPUT); //通过循环将D2~D5的功能设置为输出
      digitalWrite(i,LOW);//配置过程中保证电机停止
   }

   /*
   //当然你也可以这么写，只是不够优雅
   pinMode(2,OUTPUT);
   pinMode(3,OUTPUT);
   pinMode(4,OUTPUT);
   pinMode(5,OUTPUT);
   */

   //M1正转
   digitalWrite(2,HIGH);
   digitalWrite(3,LOW);
   delay(3000);//程序执行暂停三秒，也即保持以上状态3秒

   //M1反转
   digitalWrite(2,LOW);
   digitalWrite(3,HIGH);
   delay(3000);

   //M1停止
   digitalWrite(2,LOW);
   digitalWrite(3,LOW);
   delay(3000);

   //M2正转
   digitalWrite(4,HIGH);
   digitalWrite(5,LOW);

   //M2反转
   digitalWrite(4,LOW);
   digitalWrite(5,HIGH);
   delay(3000);

   //M2停止
   digitalWrite(4,LOW);
   digitalWrite(5,LOW);
   delay(3000);
}

```

### 继电器模块
 + 通过背面的[ULN2003](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=38966192028&_u=b2e8a0g1286c)进行驱动，由USB供电时可能供电不足。

    | 继电器  | 控制引脚 |
    |:------:| :------:|
    | 继电器1 | D12    |
    | 继电器2 | D13    |

```
void setup()
{
//必须存在的函数，该函数内代码仅会在开机时运行一次，而后除非重启不再运行

   //设置控制继电器的引脚为输出模式
   pinMode(12,OUTPUT);
   pinMode(13,OUTPUT);
   //并给他们赋上初始状态，此时COM与NC连接
   digitalWrite(12,LOW);
   digitalWrite(13,LOW);
}


void loop()
{
//该函数内的代码将会在执行完void setup()内代码后重复执行

   digitalWrite(12,HIGH); //触发继电器1，此时COM与NO连接
   delay(3000);
   digitalWrite(12,LOW);//触发继电器1，此时COM与NC连接
   delay(3000);
   digitalWrite(13,HIGH); //触发继电器1，此时COM与NO连接
   delay(3000);
   digitalWrite(13,LOW);//触发继电器1，此时COM与NC连接
   delay(3000);
}
```

### [433M遥控模块](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=572454945799&_u=b2e8a0g110db)
 + 需对应的[遥控](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.35d22e8d9VZyka&id=572454945799&_u=b2e8a0g110db)
 + 每个按键对应一个引脚信号（D6-D9）
### 双层接线端子
 + 通过背面的[NCE6020AK](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.32372e8d9Vj8ZU&id=621222203660&_u=b2e8a0g1b867)进行驱动，带防反接
 + 通过其右侧跳线帽选择输出电压（5/12V 可选）
 + L1 -> D10; L2 -> D11
  </br></br></br></br>

