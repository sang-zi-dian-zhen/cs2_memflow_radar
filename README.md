# cs2雷达	使用[memflow](https://github.com/memflow/memflow)
## 	作者 / 烟雨平生	UID : 421033640
 > ### 基于[cs2-dma-radar](https://github.com/rabume/cs2-dma-radar)
 > ### 使用AI重构为rust并使用memflow访问内存

### 视频教程	:	[补档01-CS2网页雷达使用memflow访问内存](https://www.bilibili.com/video/BV1KMjn6jEmg)
### 文字教程	:	


## 1 : **安装memflow** 
```
sudo apt install cargo
cargo install memflowup

sudo su
export PATH=/home/??普通用户名/.cargo/bin:$PATH	#临时-当前终端
memflowup pull --all	#安装到root用户
```


## 2 : **前端编译** 
```
sudo apt install npm

cd ??/cs2_memflow_radar/client

npm audit fix --force
npm run build
```


## 3 : **项目编译** 
```
cd ??/cs2_memflow_radar
cargo build --release

#VM里ssh连接运行
cd ??/cs2_memflow_radar
sudo ./target/release/cs2_radar -c qemu -o win32
```

### [无法找到 dtb](https://github.com/memflow/memflow/issues/100)	可更改为memflow-kvm连接器
### [memflow-kvm](https://github.com/memflow/memflow-kvm)模块未适配内核7.0+
### 使用仓库提供的[memflow.ko](memflow.ko)已适配内核7.0+[源码修改](源码修改)
### memflow-kvm连接器	:	

```
sudo mkdir -p /lib/modules/$(uname -r)/extra
sudo cp ??/memflow.ko /lib/modules/$(uname -r)/extra/

sudo depmod -a
sudo modprobe memflow
echo "memflow" | sudo tee /etc/modules-load.d/memflow.conf	#设置开机自启

#VM里ssh连接运行
cd ??/cs2_memflow_radar
sudo ./target/release/cs2_radar -c kvm -o win32
```





![这是图片](mmexport1781674442926.jpg "cs2雷达")

- 与之配套	[QEMU全仿真](https://github.com/sang-zi-dian-zhen/QEMU-virtual-machine-full-emulation-passes-pafish-testing)
  > 仓库属于	烟雨平生	UID : 421033640  
  > 桑梓店镇		UID : 1081527516  已测试平台2026-06-26\[完美-5E]  








