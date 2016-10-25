# MultiProcesses
php多进程工具类

### 使用步骤

在composer.json中增加
```
{
  "require": {
    "yezuozuo/multi-processes": "dev-master"
  }
}
```

然会执行
```
composer install
```

### example
1. 引入MultiProcesses类文件
2. 设置MultiProcesses参数,并创建MultiProcesses实例
3. 设置回调方法
4. 调用start();

```
<?php

require __DIR__.'/../vendor/autoload.php';

use MultiProcesses\MultiProcesses;

$worker = new MultiProcesses([
        "workerNum" => 5,
        "reActive" => true,
    ]);

$worker->function['childProcessStart'] = function($workerId, $currentPid){
    for ($i = 1; $i <= 5; $i++) {
        echo "进程编号:{$workerId} ,进程ID:{$currentPid} ,数值:{$i} " .PHP_EOL;
        usleep(100000);
    }
};
$worker->start();

```

### result
```
进程编号:0 ,进程ID:13621 ,数值:1 
进程编号:1 ,进程ID:13622 ,数值:1 
进程编号:2 ,进程ID:13623 ,数值:1 
进程编号:3 ,进程ID:13624 ,数值:1 
进程编号:4 ,进程ID:13625 ,数值:1 
进程编号:1 ,进程ID:13622 ,数值:2 
进程编号:0 ,进程ID:13621 ,数值:2 
进程编号:2 ,进程ID:13623 ,数值:2 
进程编号:3 ,进程ID:13624 ,数值:2 
进程编号:4 ,进程ID:13625 ,数值:2 
进程编号:0 ,进程ID:13621 ,数值:3 
进程编号:1 ,进程ID:13622 ,数值:3 
进程编号:2 ,进程ID:13623 ,数值:3 
进程编号:3 ,进程ID:13624 ,数值:3 
进程编号:4 ,进程ID:13625 ,数值:3 
进程编号:0 ,进程ID:13621 ,数值:4 
进程编号:1 ,进程ID:13622 ,数值:4 
进程编号:2 ,进程ID:13623 ,数值:4 
进程编号:3 ,进程ID:13624 ,数值:4 
进程编号:4 ,进程ID:13625 ,数值:4 
进程编号:0 ,进程ID:13621 ,数值:5 
进程编号:1 ,进程ID:13622 ,数值:5 
进程编号:2 ,进程ID:13623 ,数值:5 
进程编号:4 ,进程ID:13625 ,数值:5 
进程编号:3 ,进程ID:13624 ,数值:5 
进程ID:13624, 发来信号,状态:0.
进程ID:13622, 发来信号,状态:0.
进程ID:13621, 发来信号,状态:0.
进程ID:13623, 发来信号,状态:0.
进程ID:13625, 发来信号,状态:0.
主进程退出

```