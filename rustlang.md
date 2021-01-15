# Rust学习笔记
## 猜数
``` rust
use rand::Rng;
use std::cmp::Ordering; //enum
use std::io; //prelude //trait

fn main() {
    println!("猜数游戏");
    let secret_num = rand::thread_rng().gen_range(1, 101); //包括1，不包括101
    //println!("神秘数字是：{}", secret_num);

    // 循环
    loop {
        println!("请输入一个数字(0-100)：");

        // let foo = 1;
        // let bar = foo;  //immutable
        // foo = 2;

        let mut guess = String::new();

        io::stdin().read_line(&mut guess).expect("无法读取！");
        //io::Result Ok, Err

        //  shadow
        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => {
                println!("请输入数字哦！");
                continue;
            }
        };

        println!("你猜的数是：{}", guess);

        //比较数字
        match guess.cmp(&secret_num) {
            Ordering::Less => println!("Too small!"), //arm
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```
## 第3章 通用的编程概念
### 3.1 变量与可变性
* 声明变量使用`let`关键字
* 默认情况下，变量是不可变的（Immutable）
* 声明变量时，在变量前面加上`mut`，就可以使变量可变

### 变量与常量