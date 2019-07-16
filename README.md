# Enumerations lab

Fork and clone this repo. On your fork, answer and commit the follow questions. When you are finished, submit the link to your repo on Canvas.


## Question 1

a) Define an enumeration called `iOSDeviceType` with member values `iPhone`, `iPad`, `iWatch`. Create a variable called `myDevice` and assign it one member value.

```swift
enum iOSDeviceType{
    case iPhone(String)
    case iPad(String)
    case iWatch
}

var myDevice = iOSDeviceType.iPad

```
b) Adjust your code above so that `iPhone` and `iPad` have associated values of type String which represents the model number, eg: `iPhone("6 Plus")`. Use a switch case and let syntax to print out the model number of each device.

```swift
//Q1 Solution
var myDeviceB = iOSDeviceType.iPhone("6")

switch myDeviceB{
    case .iPhone(let model):
        print("iphone \(model)")
    case .iPad:
        print("")
    case .iWatch:
        print("")
}

print(myDeviceB)

```
```swift
//Q1 More elaborate solution
var myDeviceB = iOSDeviceType.iPhone("6")
var myDeviceC = iOSDeviceType.iPad("Pro 11 Inch")
var myDeviceD = iOSDeviceType.iWatch("3")

func checkMyModel(device: iOSDeviceType){
    switch device{
        case .iPhone(let model):
            print("iphone \(model)")
        case  .iPad(let model):
            print("ipad \(model)")
        case let .iWatch(model):
            print("Apple Watch Series \(model)")
    }
}

checkMyModel(device: myDeviceB)
checkMyModel(device: myDeviceC)
checkMyModel(device: myDeviceD)
```

## Question 2

a) Write an enum called `Shape` and give it cases for `triangle`, `rectangle`, `square`, `pentagon`, and `hexagon`.

b) Write a method inside `Shape` that returns how many sides the shape has. Create a variable called `myFavoritePolygon` and assign it to one of the shapes above, then print out how many sides it has.

```swift
//Q2 Part A and B

enum Shape:String{
    case triangle = "3 sides"
    case rectangle = "4 sides"
    case square = "four sides"
    case pentagon = "5 sides"
    case hexagon = "6 sides"

    func findNumberOfSides() -> String{
        switch self {
            case .triangle:
                return Shape.triangle.rawValue
            case .rectangle:
                return Shape.rectangle.rawValue
            case .square:
                return Shape.square.rawValue
            case .pentagon:
                return Shape.pentagon.rawValue
            case .hexagon:
                return Shape.hexagon.rawValue
        }
    }
}

var myFavoritePolygon = Shape.rectangle.findNumberOfSides()
print(myFavoritePolygon)
```

c) Re-write `Shape` so that each case has an associated value of type Int that will represent the length of the sides (assume the shapes are regular polygons so all the sides are the same length) and write a method inside that returns the perimeter of the shape.

```swift
//Q2 Part C

enum Shape{

    case triangle(Int)
    case rectangle(Int)
    case square(Int)
    case pentagon(Int)
    case hexagon(Int)

    func findPerimeter() -> Int{
        switch self {
            case .triangle(let length):
                return length * 3
            case .rectangle(let length):
                return length * 4
            case .square(let length):
                return length * 4
            case .pentagon(let length):
                return length * 5
            case .hexagon(let length):
                return length * 6
        }
    }
}

var lengthOfMyTriangle = Shape.triangle(10).findPerimeter()
print(lengthOfMyTriangle)


```


## Question 3

Write an enum called `OperatingSystem` and give it cases for `windows`, `mac`, and `linux`. Create an array of 10 `OperatingSystem` objects where each one is set to a random operating system. Then, iterate through the array and print out a message depending on the operating system.


```swift
enum OperatingSystem: CaseIterable {
    case windows
    case mac
    case linux
}


var something = [OperatingSystem.windows,OperatingSystem.mac,OperatingSystem.linux,OperatingSystem.linux,OperatingSystem.linux,OperatingSystem.mac,OperatingSystem.windows,OperatingSystem.mac,OperatingSystem.windows,OperatingSystem.linux]

for i in something{
    switch i {
        case .linux:
            print("It's Linux!")
        case .windows:
            print("It's Windows!")
        case .mac:
            print("It's Mac!")
    }
}

```

## Question 4

You are working on a game in which your character is exploring a grid-like map. You get the original location of the character and the steps he will take.

- A step .up will increase the y coordinate by 1.
- A step .down will decrease the y coordinate by 1.
- A step .right will increase the x coordinate by 1.
- A step .left will decrease the x coordinate by 1.
- Print the final location of the character after all the steps have been taken.

```swift
enum Direction {
    case up
    case down
    case left
    case right
}

var location = (x: 0, y: 0)
var steps: [Direction] = [.up, .up, .left, .down, .left]

// your code here
```
```swift

enum Direction {
    case up
    case down
    case left
    case right
}

var location = (x: 0, y: 0)
var steps: [Direction] = [.up, .up, .left, .down, .left]

for i in steps{
    switch i {
        case .up:
            location.1 += 1
        case .down:
            location.1 -= 1
        case .left:
            location.0 -= 1
        case .right:
            location.0 += 1
        }
    }
print(location)
```


## Question 5

a) Define an enumeration named `HandShape` with three members: `.rock`, `.paper`, `.scissors`.

b) Define an enumeration named `MatchResult` with three members: `.win`, `.draw`, `.lose`.

c) Write a function called `match` that takes two `HandShapes` and returns a `MatchResult`. It should return the outcome for the first player (the one with the first hand shape).

Hint: Rock beats scissors, paper beats rock, scissor beats paper

```swift
enum HandShape{
    case rock
    case paper
    case scissors
}

enum MatchResult{
    case win
    case draw
    case lose
}

func match(firstPlayer:HandShape,secondPlayer:HandShape)->MatchResult{
    switch firstPlayer {
        case .rock:
            switch secondPlayer {
                case .rock:
                    return MatchResult.draw
                case .paper:
                    return MatchResult.lose
                case .scissors:
                    return MatchResult.win
    }
    case .paper:
        switch secondPlayer {
            case .rock:
                return MatchResult.win
            case .paper:
                return MatchResult.draw
            case .scissors:
                return MatchResult.lose
    }
    case .scissors:
        switch secondPlayer {
            case .rock:
                return MatchResult.lose
            case .paper:
                return MatchResult.win
            case .scissors:
                return MatchResult.draw
        }
    }
}

var Jack = HandShape.paper
var Jackass = HandShape.rock

print(match(firstPlayer: Jack, secondPlayer: Jackass))
```

## Question 6

a) You are given a `CoinType` enumeration which describes different coin values. Print the total value of the coins in the array `moneyArray` which contains tuples of type (`quantity`, `CoinType`).

```swift
enum CoinType: Int {
    case penny = 1
    case nickle = 5
    case dime = 10
    case quarter = 25
}

var moneyArray:[(Int,CoinType)] = [(10,.penny),
                                   (15,.nickle),
                                   (3,.quarter),
                                   (20,.penny),
                                   (3,.dime),
                                   (7,.quarter)]

// your code here
```
```swift
//Q6 Part A

var total = 0
for i in moneyArray{
total += (i.0 * i.1.rawValue)
}; print("\(total) cents")

```

b) Write a method in the `CoinType` enum that returns an Int representing how many coins of that type you need to have a dollar. Then, create an instance of `CoinType` set to `.nickle` and use your method to print out how many nickels you need to have to make a dollar.

```swift
//Q6 Part B
enum CoinType: Int {
    case penny = 1
    case nickle = 5
    case dime = 10
    case quarter = 25

    func howManyCoinsNeededForADollar()->Int{
        switch self {
            case .penny:
        return 100
            case .nickle:
        return 20
            case .dime:
        return 10
            case .quarter:
        return 4
        }
    }
}

var answer6B = CoinType.nickle
print(answer6B.howManyCoinsNeededForADollar())
```


## Question 7

a) Write an enum called `DayOfWeek` to represent the days of the week with a raw value of type String.

b) Given the array `poorlyFormattedDays`, write code that will produce an array of enums that match the days.

`let poorlyFormattedDays = ["MONDAY", "wednesday", "Sunday", "monday", "Tuesday", "WEDNESDAY", "thursday", "SATURDAY", "tuesday", "FRIDAy", "Wednesday", "Monday", "Friday", "sunday"]`

c) Write a method in `DayOfWeek` called `isWeekend` that determines whether a day is part of the weekend or not and write code to calculate how many week days appear in `poorlyFormattedDays`. z1zxq   

```swift
enum DayOfWeek:String{
    case sunday = "sunday"
    case monday = "monday"
    case tuesday = "tuesday"
    case wednesday = "wednesday"
    case thursday = "thursday"
    case friday = "friday"
    case saturday = "saturday"

    func isWeekend()->Bool{
        switch self{
        case .sunday:
            return true
        case .monday:
            return false
        case .tuesday:
            return false
        case .wednesday:
            return false
        case .thursday:
            return false
        case .friday:
            return false
        case .saturday:
            return true
        }
    }
}

let poorlyFormattedDays = ["MONDAY", "wednesday", "Sunday", "monday", "Tuesday", "WEDNESDAY", "thursday", "SATURDAY", "tuesday", "FRIDAy", "Wednesday", "Monday", "Friday", "sunday"]

var properlyFormattedDays = [DayOfWeek]()

for i in poorlyFormattedDays{
    if let d = DayOfWeek.init(rawValue: i.lowercased()){
        properlyFormattedDays.append(d)
    }
}
var answer = properlyFormattedDays.map {$0.rawValue}
//print(properlyFormattedDays)
print(answer)

var weekendCount = 0
for i in poorlyFormattedDays{
    if let d = DayOfWeek.init(rawValue: i.lowercased()){
        if d.isWeekend() {
            weekendCount += 1
        }
    }
}; print("Number of weekends in the array: \(weekendCount)")
```

## Question 8

a) Create an enum called `MetroLine` with cases for the colors of the metro train lines. Create an instance of `MetroLine`.

b) Modify your enum so that each case has an associated value of either Character or Int that will represent the train on that line. Create a new instance of `MetroLine` and give it an appropriate train letter or number.

c) Write code that prints the train letter or number of your instance of `MetroLine`.

```swift
enum MetroLine{
    case red(Int)
    case green(Int)
    case orange(String)
}

var answerA = MetroLine.red

var answerB = MetroLine.red(1)

switch answerB {
    case .red(let number):
        print("\(number)")
    case .green(let number):
        print("\(number)")
    case .orange(let number):
        print("\(number)")
}

```

## Question 9

a) Think of your own example of something that can be modeled as an enum and write it. Remember that enums allow you to create instances of a defined list of cases.

b) Add a method to your enum.... try to have the method make sense.

```swift
enum RickSanchez{

    case Pickle
    case Tiny
    case Doofus
    case Simple

    func isAsshole()->Bool{
        switch self {
            case .Pickle:
                return true
            case .Tiny:
                return true
            case .Doofus:
                return false
            case .Simple:
                return false
        }
    }
}

var rickC137 = RickSanchez.Pickle
print(rickC137.isAsshole())
```
