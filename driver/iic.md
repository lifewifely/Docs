 

I2C有两根线，分别是SDA和SCL，所有的设备都是接到这两根线上。那么，这些设备如何知道数据是发送给它们呢？这就得依靠前面所说到的地址了。设备I2C的地址是固定的，比如0x50，0x60等等。因为只能有127个地址，地址冲突是很常见的，所以一般设备都会有一个地址选择PIN，比如拉高时候为0x50，接地为0x60。如果无论拉高还是接地，都和别的芯片有冲突，那该怎么办呢？答案是：凉拌，没办法。遇到这种情况，只能换芯片了。



（1）I2C总线相关

传输开始条件：SCL处于高电平，SDA下降沿时；

传输接收条件：SCL处于高电平，SDA上升沿时；

传输数据：开始传输后，SCL处于高电平时，SDA的数据为所传输的数据；

回应：当传输完一个字节后，I2C设备需要回应一个ACK，这样主机才继续发送；因此回应信号是在传输完8bit后的下一个数据位（SDA值），当SDA为0表示有回应，为1表示没回应；

正常I2C总线的数据是：Start + I2C devece id + R/W + ACK + Data（first byte）+ ACK + ... + Data（n）+ ACK + Stop





mcu是32bit的 halfword就是16bit，*2相当于2byte