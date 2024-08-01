# 1.常见变成概念

## 1.1变量和可变性质

```rust
fn main() {
let x = 5;
println!("The value of x is: {x}");
x = 6;
println!("The value of x is: {x}");
}
//输出的变量内容需要用{}装起来，这就像卖出商品的包装一样
//使用mut明确的标识变量是否会被改变，这一点有利于推导代码。
//
```

### 1.1.1常量

类似不可变量，常量是绑定到一个名称的不允许改变的值。

值得注意的是：

1. 不允许对常量使用mut。

2. 常量不光默认不可改变，它总是不变。

3. 声明常量使用const关键字而不是let，并且必须注明值的类型。

4. 常量可以在任何作用域中声明，包括全局作用域。

5. 常量只能被设置为常量表达式，而不可以是任何其他只能在运行时计算出的值。

   ```RUST
   const THREE_HOURS_IN_SECONDS: U32 =60*60*60;
   ```

将结果写成一组有限的操作，目的是为了更好的理解和验证此值。

在声明它的作用域之中，常量在整个程序生命周期中都有效，此属性使得常量可以作为多处代码使用的全局范围的值。

### 1.1.2隐藏（shadowing）

我们可以定义一个与之前同名的新变量，这就是隐藏。隐藏与作用域这个概念紧密相关。

```rust
fn main(){
let x=5;
let x=x+1;
{
let x=x*2;
println!("{x}");
}
println!("{x}");
}
//第一个输出的结果为12，第二个输出的结果为6
```

隐藏与将变量标记为mut是由区别的。当不小心尝试对变量重新赋值 时，如果没有使用let关键字，就会导致编译时的错误。通过使用let，我们可以用这个值进行一些计算，不过计算之后变量仍然是不可变的。

使用隐藏的时候不能带上mut，因为此时无法改变变量的类型。

## 1.2数据类型

在rust中，每一个值都属于某一个数据类型（data type），这告诉rust它被指定为何种数据。以便明确数据处理方式。我们将看到两类数据类型子集：**标量**（scalar）和**复合**（compound）。

rust属于静态类型的语言，也就是说在编译的时就必须知道所有变量的类型。当多种类型均有可能的时候，必须添加类型注解：

```rust
let guess : u32 ="42".prase().expert("Not a number");
//prase()用于将string类型转换为数字，但是数字有不同的类型所以需要告诉编译器这个变量的类型。
```

### 1.2.1标量类型

标量类型代表一个单独的值。rust中有四种基本类型标量分别是：整数，浮点型，布尔类型，字符类型。

**整数**

整数是一个没有小数部分的数字。i32代表有符号的长度为32bit的数字，而u32代表没有符号的长度为32位的数字。

若是arch类型则是isize和usize，这两种类型依赖运行程序的计算机架构。

**浮点型**

分别是两种类型：f32-单精度浮点数和f64-多精度浮点数

所有的浮点型都是有符号的。

**数值运算**

包含加减乘除取余

**布尔型**

bool标识类型，true和false代表种类

**字符类型**

chat，rust的char类型的大小分为四个字节（four bytes）

### 1.2.2复合类型

复合类型一共存在两种类型分别是：元组（tuple）和数组（array）。

**元组类型**

元组是一个将多个其他类型的值组合进一个复合类型的主要方式。

元组长度固定：一旦声明，其长度不会增大或者缩小。

例如：

```rust
let tup：（i32,f64,u8）=(500,6.4,1);
let (x,y,z)=tup;//解构操作
//也可以通过点号（.）后跟索引来直接访问他们。
tup.0；
元组的第一个索引值为0；
```

不带任何的元组有个特殊的名称，交租单元元组。

**数组类型**

数组包含的多个值类型必须相同。

rust中数组的长度是固定的。

```rust
let a:[i32;5]=[1,2,3,4,5];
let a=[3;5] //表示a数组中存在五个元素每个元素的值是5
```

交代元素类型和数目。

### 1.3函数

rust代码中的函数和变量名都是用snake case规范风格。

所有的字母都是小写并使用下划线分隔单词。rust不关心函数定义的位置，只要函数被调用时出现在调用之处可见的作用域就行。

### 1.3.1参数

我们可以定义拥有参数的函数，参数是特殊变量，是函数签名的一部分。当函数拥有参数（形参）时，可以为这些参数提供具体的值（实参）。参数需要明确表示类型

### 1.3.2语句

rust是一门基于表达式的语言。

**语句**是执行一些操作但不返回值的指令。表达式计算并产生一个值。

**表达式**

计算并产生一个值。

具体来说就是函数中不带分号的表达式可以作为返回值。

在rust中不能出现x=y=6的情况。而是使用代码块的返回值来作为赋值的对象，例如：

```rust
fn main() -> u32{
let y={
let x:u32=3;
x+1
};
}
```

在参数括号后面跟着返回值的类型。

### 1.4控制流

if**表达式**

判断条件的类型必须是bool。

if number {}这种写法在rust中成立的前提就是，number此时的类型必须是bool。

rust会用match来匹配多种情况。

**在let语句中使用if**

```rust
fn main(){
let condition =true;
let number =if condition{5}else{6};
println!("");
}
```

**使用循环重复执行**

第一个关键字：loop；

loop会一直执行代码段中的内容，此时需要break来跳出当前的动作。

```rust
'counting_up:loop{}
//通过循环标记可以让其通过break跳出到合适的位置。
```

**while**

只有当条件为真的时候才会执行，简单粗暴。

**for**

```rust
fn main(){
let a=[1,2,3,4,5];
for element in a
{
println!("{element}");
}
}
//如果需要操作每一个数组中的元素那么可以考虑使用这种用法

fn main()
{
    for number in (1..4).rev()
    {
        println!("{}");
    }
    println!("{}");
    
}
// .rev() 可以直接反转数组，好用的小技巧
```

# 2.所有权（ownership）

## 2.1什么是所有权

作为rust的核心功能之一，该概念对其他部分有着深刻的影响。

所有程序都必须管理其运行时使用的内存的方式。一些语言中存在垃圾回收机制，在程序运行时规律的寻找不再使用的内存。另一些语言中程序员必须亲自分配和释放内存。rust则选择了第三种方式：通过所有权系统管理内存。编译器在编译的时会根据一系列的规则进行检查，如果违反这些规则，程序都不能把编译。

 所有权的主要目的就是为了**管理堆数据。**

### 2.1.1所有权规则

1. **每个值都有一个所有者（Owner）**：在 Rust 中，变量拥有其值的所有权。当拥有者（owner）超出作用域时，值就会被释放。
2. **一次只能有一个可变引用或多个不可变引用**：这个规则确保在同一时间内，要么有一个可变引用（mutable reference），要么有多个不可变引用（immutable references），但不能同时拥有可变引用和不可变引用。这样的规则保证了线程安全，防止了数据竞争。
3. **所有权可以通过移动转移**：当将拥有某个值的变量赋值给另一个变量时，所有权会从一个变量移动到另一个变量。这意味着源变量将不再有效，防止了悬空引用。
4. **所有权可以通过借用（borrowing）来共享**：通过引用（references），可以在不转移所有权的情况下让多个部分访问同一份数据。
5. **所有权规则适用于所有类型**：所有权规则适用于所有类型，包括自定义类型和标准库类型。

### 2.1.2变量作用域

一个变量和其有效的作用域

1. 当变量进入作用域时，它就是有效的。
2. 这一直持续到它离开作用域为止。

### 2.1.3 String类型

```rust
fn main()
{
    let mut s = String::from("hello");
    s.push_str(", world");
    println!("{s}");
}
```

当S离开作用域后方，rust会调用一个特殊的函数名字为drop，用于释放s的内存。

### 2.1.4变量与数据交互的方式

1. **移动**

   ```rust
   fn main()
   {
       let x=5;
       let y=x;
   }
   //因为整数是已知固定大小的简单值，所以这两个5都被放入了栈中，这种操作Copy trait
   //但是当数据类型换成String的时候这个情况就不同了
   
   fn main()
   {
       let s1=String::("hello");
       let s2=s1;
   }
   //string在底层包含三部分，第一个部分是一个指针，指针的值就是string的内容，第二部分就是string的实际长度，使用了多少内存，而第三部分就是string从分配器获取了多少内存。
   //而当你使用上述赋值的情况时，会出现两种情况，第一种指针指向的value不复制，也就是说此时的s1，s2共享同一个内容，在此种情况下会出现重复释放的问题。那第二种情况就是value也赋值一份，但是这种情况就会非常影响性能。
   //因此，rust就做出了一个设定，当上述代码执行后，Rust认为s1不再有效，因此当s1离开作用域后不需要清理任何东西。
   //这里涉及一个rust的设计选择，Rust永远也不会自动创建数据的深拷贝，因此任何自动的复制都可以被认为是对运行时性能影响较小的。
   ```

   

2. 克隆

   当我们确实需要深度复制string中堆上的数据，而不仅仅是栈上的数据，我们可以使用一个**clone**的通用函数。

   ```rust
   # fn main() {
   
      let s1 = String::from("hello");
   let s2 = s1.clone();
      println!("s1 = {}, s2 = {}", s1, s2);
   
      # }
   ```
   # 
   ```rust
   
   Rust有一个叫做**Copy trait**的特殊注解，可以用在类似整型这样的类型存储来栈上，如果一个类型实现了Copy trait那么一个旧的变量再赋值给一个新的变量后本身依旧仍然可用，而不是像string的移动一样。
   
   Rust 不允许自身或其任何部分实现了 **Drop trait** 的类型使用 **Copy trait**。
   
   任何一组简单标量值的组合都可以实现copy，任何不需要分配内存或某种形式资源的类型都可以 实现copy。
   
   下面是一些Copy类型：
   
   1. 所有整数类型：u32；
   2. bool类型
   3. 所有浮点数类型：f64
   4. 字符类型：char
   5. 元组：当包含元素的类型都实现copy，那么此时可以认为元组是实现了copy。
   ```

### 2.1.5所有权函数

将值传递给函数与给变量赋值的原理类似 。向函数传递值可能会 移动或者复制，就像赋值语句一样。

```rust
fn main() {
let s = String::from("hello"); // s 进入作用域
takes_ownership(s); // s 的值移动到函数里 ...
// ... 所以到这里不再有效
let x = 5; // x 进入作用域
makes_copy(x); // x 应该移动函数里，
// 但 i32 是 Copy 的，
// 所以在后面可继续使用 x
} // 这里，x 先移出了作用域，然后是 s。但因为 s 的值已被移走，
// 没有特殊之处
```

fn takes_ownership(some_string: String) { // some_string 进入作用域
println!("{}", some_string);
} // 这里，some_string 移出作用域并调用 `drop` 方法。
// 占用的内存被释放
fn makes_copy(some_integer: i32) { // some_integer 进入作用域
println!("{}", some_integer);
} // 这里，some_integer 移出作用域。没有特殊之处
   ```

可以很明显发现，是否实现copy trait，在移动时存在很大的区别。

### 2.1.6返回值和作用域

返回值也可以转移所有权：

​```rust
	fn main()
{
    let s1 =give_ownership();    //return value
    let s2 =String::from("hello"); //s2 get ownership
    let s3=takes_and_give_back(s2); // s2 move in take_and_give_back() scope
}
// 这里，s3 移出作用域并被丢弃。s2 也移出作用域，但已被移走，
// 所以什么也不会发生。s1 离开作用域并被丢弃


   ```

变量的所有权总是遵守相同过的模式：

  将值赋予给另一个变量时移动它。当持有堆中数据值的变量离开作用域时间，其值将通过drop被清理掉，除非数据被移动为另一个变量所有。

这个规则在某些场合会显得很麻烦，例如在每一个函数中都获取所有权并接着返回所有权有些啰嗦。

问题：

1. 当我们想要函数使用一个值但不可获取所有权该怎么办呢？这涉及到引用的定义
2. 当需要多次使用一个值，每次都传进去再返回来就有点烦人。解决方法就是可以通过**元组**来返回多个值



Rust提供了一个不用获取所有权就可以使用值的功能，叫做**引用**。

## 2.2引用和借用

引用像一个指针，因为它是一个地址我们可以由此访问储存于该地址的属于其他变量的数据。与指针不同，引用确保指向某个特殊类型的有效值。

```rust
fn main() {
let s1 = String::from("hello");
let len = calculate_length(&s1);
println!("The length of '{}' is {}.", s1, len);
}
fn calculate_length(s: &String) -> usize {
s.len()
}
// 这里，s 离开了作用域。但因为它并不拥有引用值的所有权，
// 所以什么也不会发生
```

我们传递&1给calculate_length，同时再函数定义中，我们获取&string而不是string，这些符号代表的就是引用，他们允许你使用值但不获取其所有权

我们将创建一个引用的行为称为**借用** ，就像你可以借人家的东西来使用，但是实际上你没有东西的所有权，这个东西不属于你。

这里的引用也被称为**不可变引用**，这点与变量默认是不可变的一样，默认不允许修改引用的值。

### 2.2.1可变引用

既然存在不可变引用那就一定存在改变引用的方式这种凡是被称为可变引用

```rust
fn main() {
let mut s = String::from("hello");
change(&mut s);
}
fn change(some_string: &mut String) {
some_string.push_str(", world");
}
//很简单的操作，在被赋值的变量加上mut关键字，在函数的参数中带上mut关键字。

```

但是可变引用存在一个**限制**，一个变量的可变引用只能存在唯一的一个，无法创建该变量的多次可变引用。
这种限制以一种非常小心谨慎的方式允许可变性，防止同一时间对同一数据存在多个可变引用，这种限制有效的避免了**数据竞争**。
造成数据竞争的行为：

1. 两个或者更多指针同时访问同一数据。
2. 至少有一个指针被用来写入数据。
3. 没有同步数据的访问机制。

而rust避免了这种情况的发生，因为rust甚至不会编译存在数据竞争的代码。

一如既往：可以使用大括号来创建一个新的作用域，**以允许拥有多个可变引用**，只是不能**同时**拥有。

我们 **也**不能在拥有不可变引用的同时拥有可变引用。

```rust
# fn main() {
let mut s = String::from("hello");
{
let r1 = &mut s;
} // r1 在这里离开了作用域，所以我们完全可以创建一个新的引用
let r2 = &mut s;
# }
```

可以这么说不可变引用就像读数据，谁都可以同时读取数据，但是可变引用就像是既可以读取数据，又可以写数据。两者不能同时共存。

但是当不可变引用不再使用后，可以定义该变量的可变引用。（感觉已经不是传统的静态语言了）

例如：

编译器可以在作用域结束之前判断不再使用的引用，这样作用域并不会判断重叠，也就是一个变量的作用域并不是指{}内部的整体，而是到**最后一次使用**的地方

```rust
# fn main() {
let mut s = String::from("hello");
let r1 = &s; // 没问题
let r2 = &s; // 没问题
println!("{} and {}", r1, r2);
// 此位置之后 r1 和 r2 不再使用
let r3 = &mut s; // 没问题
println!("{}", r3);
# }
```

### 2.2.2悬垂引用

在具有指针的语言中，很容易通过释放内存时保留指向它的指针而错误地生成一个**悬垂指针**，这就会造成其指向的内存可能已经被分配给其他持有者。

相比之下，rust中确保引用永远不会变成悬垂状态，当你拥有一下数据的引用，编译器确保数据不会在其引用之前离开作用域。

例如：

```rust
# fn main() {
# let reference_to_nothing = dangle();
# }
#
fn dangle() -> &String { // dangle 返回一个字符串的引用
let s = String::from("hello"); // s 是一个新字符串
&s // 返回字符串 s 的引用
} // 这里 s 离开作用域并被丢弃。其内存被释放。
// 危险！
```

这是因为s是在dangle函数内创建的，当dangle的代码执行完毕后，s将被释放。不过我们尝试返回它的引用，这意味着这个引用会指向一个无效的String，这是编译器绝对不会允许的。

修改方法是不返回引用直接将数据的所有权返回这样值就没有被释放。

### **2.2.3** **引用的规则**

让我们概括一下之前对引用的讨论：

• 在任意给定时间，**要么**只能有一个可变引用，**要么**只能有多个不可变引用。

• 引用必须**总是**有效的。

接下来，我们来看看另一种不同类型的引用：**slice**。

slice 允许你引用集合中一段连续的元素序列，而不用引用整个集合。slice是一类引用，所以他没有所有权，

指向字符串中的一部风，当你获取索引后，可以直接把字符串截取出来很好用的功能，用法是：

**let** hello = &s[0..5];

**let** world = &s[6..11];

&s[0..2] =  &s[..2]  初始索引如果不写的话那么直接从0开始。

ASCII 字符集 与使用字符串存储 UTF-8 编码的文本”， 两者存在本质的区别，这是因为UTF-8中某些字符并不是单字符存储的。

```rust
fn first_word(s: &String) -> &str {
let bytes = s.as_bytes();
for (i, &item) in bytes.iter().enumerate() {
if item == b' ' {
return &s[0..i];
}
}
&s[..]
}

```

高效。

**字符串字面值就是slice**

字符串字面值呗存储在二进制文件中，现在知道了slice了，我们就可以正确理解字符串字面值了：

let s= “Hello world”;

这里s的类型是&str，它指向二进制程序特定的位置的slice。这也就是为什么字符串字面值都是不可变的；&str是一个不可变引用。

字符串slice作为参数

不要使用&String作为参数，&str更加通用，可以适用&string这种情况。这等加于整个“String”的slice。

**其他类型的slice**

```rust
let a = [1, 2, 3, 4, 5];
let slice = &a[1..3];
assert_eq!(slice, &[2, 3]);
```

总结：

所有权，借用和slice这些概念让rust程序在编译的时候确保内存安全。Rust语言提供了跟其他系统编程语言相同的方式来控制你的内存。但拥有数据所有者在离开作用域后自动清除其数据的功能意味着你无需额外编写和调试相关功能的控制代码。

所有权系统影响了Rust中很多其他部分的工作方式，所以我们还会继续讲到这些概念，接下来让我们学习如何将多份数据组合进一个**struct**中。

# 3.使用结构体组织关联的数据

## 3.1结构体的定义和实例化

结构体和我们在元组类型的部分讨论过的元组类似，但是元组的数据组织存在顺序，类似first，second来访问其中的元素，而结构中每个成员都存在对应的名字，因此我们可以更加方便的访问结构体中的数据。

定义结构体，需要使用struct关键字并为整个结构体提供一个名字。结构体的名字需要描述它所组合的数据的意义。接着，在大括号中，定义每一部分数据的名字和类型，我们称之为字段field。例如，

```rust
struct User {
active: bool,
username: String,
email: String,
sign_in_count: u64,
}
```

一旦定义结构体后，为了使用它，通过为每个字段指定具体值来创建这个结构体的实例。创建一个实例需要以结构体的名字开头，接着在大括号中使用key：value键-值对的形式提供字段，其中key是字段的名字，value是需要存储在字段中的数据值。实例中字段的顺序不需要和他们在结构体中声明的顺序一致，换句话说，结构体的定义就像一个类型的通用模板，而实例则会在这个模板中放入特定数据来创建这个类型的值。例如：

```rust
# struct User {
# active: bool,
# username: String,
# email: String,
# sign_in_count: u64,
# }
#
fn main() {
let user1 = User {
active: true,
username: String::from("someusername123"),
email: String::from("someone@example.com"),
sign_in_count: 1,
};
}

user1.email = String::from("anotheremail@example.com");
```

采取.来获取结构体的数据。但是存在一个前提：整个实例必须是可变的；rust并不允许只将某个字段标记为可变的。另外需要注意同其他任何表达式一样，我们可以在函数体的最后一个表达式中构造一个结构体的新实例，来隐式地返回这个实例。

```rust
fn build_user(email: String, username: String) -> User {
User {
active: true,
username: username,
email: email,
sign_in_count: 1,
}
}
```

**字段初始化简写语法**（*field init shorthand*）

```rust
fn build_user(email: String, username: String) -> User {
User {
active: true,
username,
email,
sign_in_count: 1,
}
}
#
# fn main() {
# let user1 = build_user(
# String::from("someone@example.com"),
# String::from("someusername123"),
# );
# }
```

使用旧实例的大部分值但改变其部分值来创建一个新的结构实例通常是很有用的。这可以通过结构体更新语法实现。

```rust
struct User{
    active:bool,
    username:String,
    email:String,
    sign_in_count:u64,
}
fn main ()
{
    let user1= User{
        email:String::from(""),
        username:String::from(""),
        active:true,
        sign_in_count:1,
    }
    let user2=User{
        active:user1.active
        username:User1.username,
        email:String:;from(""),
        sign_in_count:User1.sign_in_count,
    }
    // 
    let user3 = User {
email: String::from("another@example.com"),
..user1
        //..User1必须放在成员赋值的最后，以指定其余的字段应从user1的相应字段中获取值。
};
}
```

请注意：**结构更新语法就像带有= 的赋值，因为它引动了数据**。总体上说我们在创建user2后就不能再使用user1了，因为user1的username字段的String被移动到了user2中。如果我们给user2后不能再使用user1了，因为赋予新的String值，从而只使用user1的active和sign_in_count值，那么user1再创建user2后仍然有效。avtive和sign_in_count的类型是实现Copy trait的类型，所以这符合克隆的规则。

### 3.1.2使用没有命名字段的元组结构来创建不同的类型

也可以定义与元组类似的结构体，称为元组结构体（tuple struct）。元组结构体有着结构体名称提供的含义，但没有具体的字段名，只有字段的类型，当你想给整个元组取一个名字，并使元组成为与其他元组不同的类型时，元组结构是很有用的，这时就像常规结构体那样为每个字段命名就显得多余和形式化了。

要定义元组结构体，以struct关键字和结构体名开头并后跟元组中的类型。例如下面两个分别叫做Color和Point元组结构体的定义和用法：

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);
fn main() {
let black = Color(0, 0, 0);
let origin = Point(0, 0, 0);
}
```

元组结构体不同的名字，即使其中的元素种类完全相同但是两者也是同的数据结构，比如一个获取Color类型参数的函数不能结构Point作为参数，元组结构体实例类似元组，既可以将他们解构为单独的部分，也可以使用点号后跟索引来访问单独的值，等等。

### 3.1.3没有任何字段的类单元结构体

我们也可以定义一个没有任何字段的结构体！他们被称为类单元结构体，因为他们类似于（），即元组类型一节中提到的unit类型。类单元结构体常常在你想要在某个类型上实现trait但不需要在类型中存储数据的时候发挥作用。

```rust
struct AlwaysEqual;
fn main() {
let subject = AlwaysEqual;
}
```

后续会介绍其用法。

### 3.1.4结构体数据的所有权

在**生命周期**中会涉及到，String类型存在所有权，而&str：slice类型没有所有权，可以使结构体存储被其他对象拥有的数据的引用，不过这么做的话需要用上生命周期，生命周期确保结构体引用的数据有效性跟结构体引用的数据有效性跟结构体本身保持一致。

用结构体的引用来作为函数的参数，这样就可以借用结构体内部的数据了，而不是获取其所有权。

### 3.1.5通过派生trait增加使用功能

Rust确实包含了打印出调式信息的功能，不过我们必须为结构体显式选择这个功能。

```rust
#[derive(Debug)]
println!("{:?}",rect1);
println!("{:#?}",rect1);//当数据比较多的时候，输出的表现效果会更好
或者使用dbg!宏
但是两者存在差异，dbg!宏接受一个表达式的所有权(与println!相反，后者接受引用)
```

## 3.2方法语法

```rust
#[derive(Debug)]
struct Rectangle{
    width:u32,
    heigh:u32,
}
impl Rectangle
{
    fn area(&self)-> u32{
        self.width*self.heigh
    }
}

fn main() 
{
let rect1=Rectangle{
    width:30,
    heigh:50,
};
println!("{}",rect1.area());
}
self是&Self的缩写
```

Rust并没有一个与->等效的运算符号，Rust有一个叫自动引用和解引用的功能：当使用object.something()调用方法时,Rust会自动为object添加&，&mut或者*，以便使object与方法签名匹配。也就是说这些代码是等价的，

```rust
#[derive(Debug,Copy,Clone)]
struct Point
{
    x:f64,
    y:f64,
}
impl Point{
    fn distance(&self,other:&Point)->f64{
        let x_squared=f64::powi(other.x-self.x,2);
        let y_squared = f64::powi(other.y - self.y, 2);
        f64::sqrt(x_squared + y_squared)
    }
}
# let p1 = Point { x: 0.0, y: 0.0 };
# let p2 = Point { x: 5.0, y: 6.5 };

p1.distance(&p2);
(&p1).distance(&p2);
```

在给出接收者和方法名的前提下，Rust可以明确地计算出方法是仅仅读取（&self），做出修改（&mut self）或者是获取所有权（self）。事实上，Rust对方法的接收者的隐式借用让所有权在实践中更友好。

### 关联函数

所有在impl块中定义的函数被称为关联函数，因为它们与impl后面命名的类型相关。我们可以定义不以self为第一参数的关联函数（所以不叫方法），因为他们并不作用于一个结构体的实例。

不是方法的关联函数经常被用作返回一个结构体新实例的构造函数。这些函数的名称通常为 new ，但 new 并不是一个关键字。

```rust
# #[derive(Debug)]
# struct Rectangle {
# width: u32,
# height: u32,
# }
#
impl Rectangle {
fn square(size: u32) -> Self {
Self {
width: size,
height: size,
}
}
}
#
# fn main() {
# let sq = Rectangle::square(3);//这里用的是：：来调用这个关联函数。
# }

```

### 多个impl块

每个结构体都允许拥有多个 impl 块。例如，示例 5-16 中的代码等同于示例 5-15，但每个方法有其自己 的 impl 块。

结构体让你可以创建出在你的领域中有意义的自定义类型。通过结构体，我们可以将相关联的数据片段 联系起来并命名它们，这样可以使得代码更加清晰。在 impl 块中，你可以定义与你的类型相关联的函 数，而方法是一种相关联的函数，让你指定结构体的实例所具有的行为。 但结构体并不是创建自定义类型的唯一方法：让我们转向 Rust 的枚举功能，为你的工具箱再添一个工具。

# 枚举

结构体给予你将字段和数据聚合在一起的方法，像 Rectangle 结构体有 width 和 height 两个字段。

而 枚举给予你将一个值成为一个集合之一的方法。

```rust
enum IpAddrKind {
V4,
V6,
}
# fn main() {
# let four = IpAddrKind::V4;
# let six = IpAddrKind::V6;
#
# route(IpAddrKind::V4);
# route(IpAddrKind::V6);
# }
fn route(ip_kind: IpAddrKind) {}


# fn main() {
enum IpAddrKind {
V4,
V6,
}
struct IpAddr {
kind: IpAddrKind,
address: String,
}
let home = IpAddr {
kind: IpAddrKind::V4,
address: String::from("127.0.0.1"),
};
let loopback = IpAddr {
kind: IpAddrKind::V6,
address: String::from("::1"),
};
# }

# fn main() {
enum IpAddr {
V4(String),
V6(String),
}
let home = IpAddr::V4(String::from("127.0.0.1"));
let loopback = IpAddr::V6(String::from("::1"));
# }
我们直接将数据附加到枚举的每个成员上，这样就不需要一个额外的结构体了。这里也很容易看出枚举工作的另一个细节：我们每一个定义的枚举成员大的名字也变成了构建枚举的实例的函数。
```

枚举类型也可以定义其方法：这一点与结构体非常相似

```rust
# fn main() {
# enum Message {
# Quit,
# Move { x: i32, y: i32 },
# Write(String),
# ChangeColor(i32, i32, i32),
# }
#
impl Message {
fn call(&self) {
// 在这里定义方法体
}
}
let m = Message::Write(String::from("hello"));
m.call();
# }
```

### Option枚举和其相对于空值的优势

Option 类型应用广泛因为 它编码了一个非常普遍的场景，即一个值要么有值要么没值。

```rust
enum Option<T> {
None,
Some(T),
}
只要一个值不是 Option<T> 类型，你就 可以安全的认定它的值不为空。这是 Rust 的一个经过深思熟虑
的设计决策，来限制空值的泛滥以增加 Rust 代码的安全性。

```

### match控制流结构

Rust有一个叫做match的极为强大的控制流运算符，它允许我们将一个值与一系列的模式相比较，并根据相匹配的模式执行相应的代码。模式可由字面值，变量，通配符和许多其他内容构成。

```rust
enum Coin{
    Penny,
    Nickel,
    Dime,
    Quarter,
}
fn value_in_cents(coin:Coin)->u8{
    match coin{
        Coin::Penny =>1,
        Coin::Nickel =>5,
        Coin::Dime=>10,
        Coin::Quarter =>25,
    }
}
```

Rust中的匹配时穷尽的，必须穷尽到最后的可能性来使代码有效。

### 通配模式和_占位符号

```rust
# fn main() {
let dice_roll = 9;
match dice_roll {
3 => add_fancy_hat(),
7 => remove_fancy_hat(),
other => move_player(other), //other会被使用
}
fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn move_player(num_spaces: u8) {}
# }


# fn main() {
let dice_roll = 9;
match dice_roll {
3 => add_fancy_hat(),
7 => remove_fancy_hat(),
_ => reroll(), //占位符 或者可以写成 _ => (),
}
fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn reroll() {}
# }
```

### if let 简洁控制流

if lei 语法让我们以一种不那么冗长的方式结合if和let，来处理只匹配一个模式的值而忽略其他模式的情况。

```rust
# fn main() {
let config_max = Some(3u8);
if let Some(max) = config_max {
println!("The maximum is configured to be {}", max);
}
# }
换句话说，可以认为 if let 是 match 的一个语法糖，它当值匹配某一模式时执行代码而忽略所有其他值。
```

用于解决match使用起来过于啰嗦的情况。

### 使用包，Crate和模块管理不断增长的项目

这里有一个需要说明的概念 ” 作用域（scope）”：代码所在的嵌套上下文有一组定义为 ”in scope” 的名 称。

Rust有许多功能可以让你管理代码的组织，包括哪些内容可以被公开，哪些内容作为私有部分，以及程序每个作用域的名字，这系统功能被统称为模块系统，包括，
包：（Packages）：cargo的一个功能，允许你构建，测试和分享crate

Crates：一个模块的树形结构，它形成了库或者二进制文件

模块：（Modules）和use，允许你控制作用域和路径的私有性。

路径（path):一个命名例如结构体，函数或者模块等项的方式

### 包和Crate

crate是rust编译时的最小单位。
cargo new project 来创建项目
cargo build project 来编译项目
cargo run 来运行项目

### 定义模块来控制作用域与私有性

从crate根节点开始寻找需要被编译的代码，通常对于一个库crate而言是src/lib.rs,对于一个二进制crate而言是src/main.rs

```powershell
New-Item -ItemType File -Name lib.rs 在当前目录下创建文件
```

声明模块：在crate根节点以外的其他文件中，你可以定义子模块。

模块中的代码路径：一旦一个模块是你crate的一部分，你可以在隐私规则允许的前提下，从同一个crate内的任意地方，通过代码路径引用该模块的代码。

私有vs公有：一个模块里的代码默认对其父模块私有。为了使一个模块公用，应当在声明时使用pub mod 代替mod。为了使一个公用模块内部的成员公用，应当在声明前使用pub。

use关键字：在作用域内，use关键字创建了一个成员的快捷方式，用来减少长路径的重复。在任何可以引用

```rust
mod front_of_house{
    mod hosting{
        fn add_to_waitlist(){

        }
        fn seat_at_table(){

        }
    }
    mod serving{
        fn take_order(){

        }
        fn serve_order() {}
        fn take_payment() {}
    }
}
```

mod称为模块。

父模块中的项不能使用子模块的私有项，但是子模块中的项可以使用他们父模块中的项，这是因为子模块封装并隐藏了他们的实现详情。

模块上的pub关键字只允许其父模块使用它，而不允许访问内部代码。

### super开始的相对路径

```rust
fn deliver_order() {}
mod back_of_house {
fn fix_incorrect_order() {
cook_order();
super::deliver_order();
}
fn cook_order() {}
}
//有一种返回上层的感觉
```

### 创建公有的结构体和枚举

如果我们在一个结构体定义的面前使用了pub，那么这个结构体会变成公有的，但是这个结构体的字段任然是私有的！

```rust
mod back_of_house{
    pub struct Breakfast{
        pub toast:String,
        seasonal_fruits:String,
    }
    impl Breakfast {
        pub fn summer(toast:&str)->Breakfast{
            Breakfastz{
                toast:String::from(toast),
                seasonal_frust:String::from("peaches"),
            }
        }
    }
}
pub fn eat_at_restaurant(){
    let mut meal =back_of_house::Breakfast::summer("Rye");
    meal.toast=String::from("wheat");
    println!("{}",meal.toast);
}
```

因为back_of_house::Breakfast结构体的toast字段是公有 的，所以我们可以在eat_at_restaurant中使用点号来随意的读写toast字段，但是不能使用私有的字段。

以为结构体中存在私有的字段，那么这个结构体需要提供一个公共的关联函数来构造Breakfast的实例，因为我们不能在模块外部的函数中设置私有字段的值。

但是，相反的是如果我们将一个枚举设置为公有，那么枚举中的所有成员都会变成公有。

默认情况下我们会将结构体的成员视为全部私有，如果没有pub关键字，而枚举类型的成员就是全部公有，两者做了一个区分。

### 使用use关键字将路径引入作用域

注意use只能创建use所在的特定作用域内的短路径。

```rust
mod front_of_house {
pub mod hosting {
pub fn add_to_waitlist() {}
}
}
use crate::front_of_house::hosting::add_to_waitlist;
pub fn eat_at_restaurant() {
add_to_waitlist();
}
//使用示例
```

有时我们会遇到一个情况：
那就是我们想使用 use 语句将两个具有相同名称的项带入作用域

```rust
use std::fmt;
use std::io;
fn function1() -> fmt::Result {
// --snip--
# Ok(())
}
fn function2() -> io::Result<()> {
// --snip--
# Ok(())
}
//解决方案就是给以名字一个新的名字，使用as关键字
use std::fmt::Result;
use std::io::Result as IoResult;
fn function1() -> Result {
// --snip--
# Ok(())
}
fn function2() -> IoResult<()> {
// --snip--
# Ok(())
}
```

### 使用pub as重导出名称

使用use关键字，将某一个名称导入当前的作用域后，这个名称在作用域中就可以使用了，但它对此作用域之外还是私有的，如果想要其他人调用我们的代码时，也能正常使用这个名称，就好像它本来就在当前作用域一样，那我们就可以将pub和use合起来使用。这种技术被称为重导出。我们不仅将一个名称导入了当前作用域，还允许别人把它导入他们自己的作用域。

### 使用外部包

需要再Cargo.toml文件中添加需要使用的包，然后通过use 引入包就可以了。

### 嵌套路径来消除大量的use行

```rust
use std::{cmp::Ordering, io};
use std::io::{self, Write};

```

### 通过glob运算符将所有的公有定义引入作用域

```RUST
use std::collections::*;
```

这个 use 语句将 std:: collections 中定义的所有公有项引入当前作用域。

### 将模块拆分成多个文件

## 常见集合

Rust标准库中包含一系列被称为**集合**的非常有用的数据结构。大部分其他数据类型都代表一个特定的值，不过集合可以包含多个值。（数组？）

不同于内建的数组和元组类型，这些集合指向的数据是存储再堆上的，这意味着数据的数量不必在编译的时候就已知。

广泛使用的集合分为三个：
**vector**：允许我们一个挨着一个地存储一系列数量可变的值。
**string**：是字符的集合。
**哈希map**：键和值。

### 使用 Vector 储存列表

