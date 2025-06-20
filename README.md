# php_mt_seed-windows
需要用命令行启动
在当前目录下打开控制台
# 运行示例：
php_mt_seed.exe 1234567890

结果（可以推算不同版本的php）：
Pattern: EXACT
Version: 3.0.7 to 5.2.0
Found 0, trying 0x14000000 - 0x17ffffff, speed 10485.8 Mseeds/s
seed = 0x16a5ea62 = 379972194 (PHP 3.0.7 to 5.2.0)
seed = 0x16a5ea63 = 379972195 (PHP 3.0.7 to 5.2.0)
Found 2, trying 0xfc000000 - 0xffffffff, speed 16911.4 Mseeds/s
Version: 5.2.1+
Found 2, trying 0x16000000 - 0x17ffffff, speed 209.0 Mseeds/s
seed = 0x174b0763 = 390793059 (PHP 5.2.1 to 7.0.x; HHVM)
Found 3, trying 0x4c000000 - 0x4dffffff, speed 175.5 Mseeds/s
seed = 0x4cc6f574 = 1288107380 (PHP 5.2.1 to 7.0.x; HHVM)
seed = 0x4cc6f574 = 1288107380 (PHP 7.1.0+)
Found 5, trying 0xfe000000 - 0xffffffff, speed 156.0 Mseeds/s
Found 5

# 高级用法（匹配范围）：
php_mt_seed.exe 1000000 2000000 0 9999999
<观察到的随机数值下限> <观察到的随机数值上限> <原始范围下限> <原始范围上限>

1000000 (第一个参数)
这是你实际观察到的随机数值的下限
表示你期望种子生成的随机数至少大于等于这个值
示例中：随机数至少是1,000,000

2000000 (第二个参数)
这是你实际观察到的随机数值的上限
表示你期望种子生成的随机数最多小于等于这个值
示例中：随机数最大是2,000,000
与第一个参数共同定义目标区间：1,000,000 ≤ rand ≤ 2,000,000

0 (第三个参数)
这是PHP代码中mt_rand()函数的原始范围下限
对应PHP代码：mt_rand(0, ...)中的第一个参数
表示随机数生成器的理论最小值

9999999 (第四个参数)
这是PHP代码中mt_rand()函数的原始范围上限
对应PHP代码：mt_rand(..., 9999999)中的第二个参数
表示随机数生成器的理论最大值

假设你在PHP代码中看到这样的调用：
$random = mt_rand(0, 9999999); 

你想找回生成这个随机数的种子，但不知道确切值，只知道：

随机数在1,000,000到2,000,000之间
原始范围是0到9,999,999
这时就可以使用： php_mt_seed.exe 1000000 2000000 0 9999999、
