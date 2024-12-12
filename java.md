## 9장

| 스택    | 힙       |
| ----- | ------- |
| 메서드   | 객체      |
| 로컬 변수 | 인스턴스 변수 |

### 1. **인스턴스 변수**

- **정의**: 클래스에 정의된 변수로, 각 객체가 독립적으로 가지는 속성입니다.
- **저장 위치**: **힙(Heap)** 메모리에 저장됩니다.
    - 객체가 생성되면 인스턴스 변수는 해당 객체의 일부로 힙 메모리에 저장됩니다.
    - 객체가 더 이상 필요 없어지면 가비지 컬렉션에 의해 메모리에서 제거됩니다.
- **생명주기**: 객체가 살아있는 동안 유지됩니다.
- **특징**: 클래스 내부에서 선언되지만 메서드나 생성자 외부에서 정의됩니다.
```java
class Example {
    int instanceVar; // 인스턴스 변수
}
```
### 2. **로컬 변수**

- **정의**: 메서드, 생성자, 또는 블록 내부에서 선언된 변수입니다.
- **저장 위치**: **스택(Stack)** 메모리에 저장됩니다.
    - 메서드가 호출되면 로컬 변수가 생성되고, 메서드 실행이 끝나면 자동으로 제거됩니다.
- **생명주기**: 메서드가 실행되는 동안에만 유효합니다.
- **특징**: 반드시 초기화되어야 사용 가능합니다.
```java
class Example {
    void method() {
        int localVar = 10; // 로컬 변수
    }
}
```

### 스택, 힙 종합 정리
```java
class Example {
    int instanceVar; // 인스턴스 변수 (힙에 저장)
    
    void method() {
        int localVar = 10; // 로컬 변수 (스택에 저장)
        Example obj = new Example(); // 객체 (힙에 저장)
    }
}
```

- 생성자를 private 로 선언 하는 것 **싱글 턴 패턴**


## 10장
### Matn 메서드 종류
- Math.abs()
주어진 인자의 절댓값을 리턴 합니다.
```java
int x = Math.abs(-240); // 240 이 리턴 됩니다.
```

- Math.random()
0.0이상 1.0 미만의 double 값을 리턴합니다.
```java
double r1 = Math.random();
int r2 = (int) (Math.random() * 5); // 0.0 ~ 5.0 (0.0이상 5,0미만)
```

- Math.round()
주어진 수를 반올림해서 가장 가까운 int 또는 long을 리턴 합니다.
```java
// f를 추가하지 않으면 double 로 간주해서 long으로 리턴합니다.
int x = Math.round(-24.8f); -25가 리턴 됩니다.
int x = Math.round(24.45f); 24가 리턴 됩니다.

long x = Math.round(24.45); 24가 리턴 됩니다.
```

- Math.min()
두 인자 중 더 작은 값을 반환 합니다. 모든 실수 사용 가능 
```java
int x = Math.min(24,240);
double x = Math.min(123123.0,123123.24);
```

- Math.max()
두 인자 중 더 큰 값을 반환 합니다. 모든 실수 사용 가능 
```java
int x = Math.max(24,240);
double x = Math.max(123123.0,123123.24);
```

- Math.sqrt()
주어진 인자의 양의 제곱근을 리턴 합니다.
```java
double x = Math.sqrt(9);
double x = Math.sqrt(42.0);
```

### 원시 변수를 사용하는 ArrayList
```java
public void autoboxing(){
	int x = 32;
	ArrayList<Integer> list = new ArrayList<>;
	list.add(x);
	int num = list.get(0); // 32 가 반환됩니다.
}
<Integer> 에 들어갈 수 있는 값들
- Boolean
- Byte
- Character
- Short
- Integer
- Long
- Float
- Double
```

### 숫자 포매팅
- String.format();
```java
public void TestFormats(){
	public static void main(String[] args){
		long myBillion = 1000000000;
		String s = String.format("%,d", myBillion);
		System.out.println(s); // 1,000,000,000 로 출력 됨

		String.format("%tc", new Date()); // Sun Nov 28 14:52:41 MST 2004
		String.format("%tr", new Date()); // 03:01:47 PM
		String.format("%tA, %<tB %<td ", new Date()); // Sunday, November 28s

		Calander cal = Calander.getInstance();
	}
}
```
- 사용방법
	- % , 6 . 1 f 
	- , 플래그 | 6 너비 | .1정밀도 | f 타입 
- 타입 
	- %d, %f, %x, %c


## 11장
### 제네릭 사용방법
- 제네릭에서의 extends 키워드는 확장(extends) 와 구현 (implements)를 모두 의미 합니다.
```java
public<T extends Animal> void takeThing(ArrayList<T> list)
- ArrayList<Cat>, ArrayList<Dog> 객체도 list에 대입 가능

public void takeThing(ArrayList<Animal> list) 
- ArrayList<Animal> 객체만 list에 대입 가능

public static <T extends Comparable<? super T>> void sort(List<T> list)
- Comparable 제네릭은 타입 매개변수가 최소한 T 클래스 또는 T의 상위 클래스 여야한다.
- Comparable을 구현하는 T 클래스 객체 사용가능
```

### ArrayList.sort() 사용 방법
```java
import java.util.ArrayList;

public class Example {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("Banana");
        list.add("Apple");
        list.add("Cherry");

        // 람다를 사용한 알파벳 순 정렬
        list.sort((o1, o2) -> o1.compareTo(o2));

        System.out.println(list); // [Apple, Banana, Cherry]
    }
}
```

### Collections.sort() 사용 방법

- Comparable을 사용하여 기본 정렬 정의
	클래스에 기본 정렬 기준을 정의하고 싶다면 `implements Comparable<T>`와 `compareTo` 메서드를 구현합니다.
```java
class Song implements Comparable<Song> { // Comparable 구현
    String title;
    String artist;

    // Constructor
    public Song(String title, String artist) {
        this.title = title;
        this.artist = artist;
    }

    // Getters
    public String getTitle() {
        return title;
    }

    public String getArtist() {
        return artist;
    }

    // compareTo 구현: Title을 기준으로 정렬
    @Override
    public int compareTo(Song s) {
        return this.title.compareTo(s.getTitle());
    }
}
// 사용
public class Main {
    public static void main(String[] args) {
        ArrayList<Song> songList = new ArrayList<>();
        songList.add(new Song("Bohemian Rhapsody", "Queen"));
        songList.add(new Song("Imagine", "John Lennon"));
        songList.add(new Song("Let It Be", "The Beatles"));

        // Title 기준으로 정렬
        Collections.sort(songList);

        // 출력
        for (Song song : songList) {
            System.out.println(song.getTitle() + " by " + song.getArtist());
        }
    }
}
```


- Comparator 사용 Comparable을 구현하지 않는 클래스를 정렬하고 싶다면?
	특정 정렬 기준이 필요할 때 `Comparator`를 별도의 클래스나 람다로 구현합니다.
```java
class Song {
    private String title;
    private String artist;

    // Constructor
    public Song(String title, String artist) {
        this.title = title;
        this.artist = artist;
    }

    // Getters
    public String getTitle() {
        return title;
    }

    public String getArtist() {
        return artist;
    }

}

class ArtistComparator implements Comparator<Song> {
    @Override
    public int compare(Song one, Song two) {
        return one.getArtist().compareTo(two.getArtist());
    }
}


// 사용
public class Main {
    public static void main(String[] args) {
        List<Song> songList = new ArrayList<>();
        songList.add(new Song("Let It Be", "The Beatles"));
        songList.add(new Song("Bohemian Rhapsody", "Queen"));
        songList.add(new Song("Imagine", "John Lennon"));

        // Artist 기준으로 정렬
        ArtistCompare artistCompare = new ArtistCompare();
        Collections.sort(songList, artistCompare);
        
        // 람다 표현식으로 처리
        Collections.sort(songList, (one, two) 
	        -> one.getArtist().compareTo(two.getArtist())
        );
    }
}

```

### HashMap 사용 방법
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Kathy",123);
scores.put("Bert",123);
scores.put("Skyler",123);

int bertScore = scores.get("Bert");
// bertScore = 123
```

### set을 사용시 중복된 항목이 들어가는 것을 방지한다.
### record 사용 방법 
```java
// 자동으로 매개변수의 getter/setter 르 ㄹ정의 해줌
record Person(int age, String name) implements Comparable<Person>{}
```

### 와일드 카드
- 두가지 다 동일한 방식입니다.
```java
public<T extends Animal> void takeThing(ArrayList<T> list);

// • 와일드카드를 쓸 때는 목록에 새로운 원소를 추가할 수 없음
public void takeThing(ArrayList<? extends Animal> list);
```


## 12장
### 컬렉션의 `forEach()` 메서드
```java
List<String> allColor = List.of("red","blue","green");
// 원소 차례대로 출력
allColor.forEach(item -> System.out.println(item));
```

### stream 사용하기
#### stream 선언
```java
List<String> strings = List.of("i", "am", "a", "list", "of", "strings");

Stream<String> stream = strings.stream(); // strings의 stream 가져오기
```
#### 중간연산
- filter() -> 주어진 조건에 맞는 원소만 스트림에 남긴다.
``` java
Stream<String> filtered = stream.filter(s -> s.startsWith("a"));
```
- skip() -> 스트림 앞쪽에서 처리하지 않을 원소의 개수를 지정한다.
``` java
Stream<String> skipped = stream.skip(2);  // 첫 2개의 원소를 건너뜀
```
- limit() -> 스트림에서 처리할 최대 원소의 개수를 지정한다.
``` java
Stream<String> limited = stream.limit(3);  // 첫 3개의 원소만 처리
```
- distinct() -> 중복된 원소를 제거한다.
``` java
Stream<String> distinct = stream.distinct();  // 중복된 원소를 제거
```
- sorted() -> 스트림의 결과를 정렬할 방법을 지정한다.
``` java
Stream<String> sorted = stream.sorted();  // 기본적으로 오름차순 정렬
```
- map() -> 스트림의 각 원소를 주어진 함수로 변환한다.
``` java
Stream<String> mapped = stream.map(s -> s.toUpperCase());  // 각 원소를 대문자로 변환
```
- dropWhile() -> 조건이 **참**인 동안의 원소를 건너뛰고, 이후 원소만 처리한다.
``` java
Stream<String> dropped = stream.dropWhile(s -> s.length() < 4);  // 길이가 4 미만인 원소를 건너뜀
```
- takeWhile() -> 조건이 **참**인 동안의 원소만 처리하고, 이후 원소는 무시한다.
``` java
Stream<String> taken = stream.takeWhile(s -> s.length() < 4);  // 길이가 4 미만인 원소만 처리
```

#### 최종 연산
- count() -> 스트림의 요소 개수를 셉니다.
```java
long count = stream.count();
```
- collect -> 스트림의 최종 연산 중 하나로, 데이터를 처리한 후 그 결과를 수집하여 반환하는 역할을 합니다.
```java
List<String> list = stream.collect(Collectors.toList());
```
- min() / max() -> 스트림의 요소들 중 최소값(`min()`) 또는 최대값(`max()`)을 찾는 연산입니다.
```java
Optional<String> min = stream.min(String::compareTo); 
Optional<String> max = stream.max(String::compareTo);
```
- anyMatch() -> 조건을 만족하는 요소가 하나라도 있으면 `true`를 반환합니다.
```java
boolean anyMatch = stream.anyMatch(s -> s.startsWith("a"));
```
- allMatch() -> 모든 요소가 조건을 만족해야 `true`를 반환합니다.
```java
boolean allMatch = stream.allMatch(s -> s.length() > 2);
```
- noneMatch() ->조건을 만족하는 요소가 하나도 없으면 `true`를 반환합니다. 
```java
boolean noneMatch = stream.noneMatch(s -> s.isEmpty());
```
- findFirst() / findAny() -> 스트림의 첫 번째 요소 또는 임의의 요소를 반환하는 연산입니다.
```java
Optional<String> first = stream.findFirst();
Optional<String> any = stream.findAny();
```
- **`sum()` / `average()` / `min()` / `max()`** (특정 타입에 대해서만 사용 가능) -> 스트림의 숫자형 요소들에 대해 합계, 평균, 최소값, 최대값을 구하는 연산입니다.
```java
int sum = stream.mapToInt(Integer::intValue).sum();
OptionalDouble average = stream.mapToInt(Integer::intValue).average();
OptionalInt min = stream.mapToInt(Integer::intValue).min();
OptionalInt max = stream.mapToInt(Integer::intValue).max();
```
- forEach()
```java
Stream<String> stream = Stream.of("red", "blue", "green");
stream.forEach(item -> System.out.println(item));  // 스트림에서의 forEach
```

최종 연산은 **스트림을 소모**합니다. 즉, 최종 연산이 실행된 후 스트림은 더 이상 사용할 수 없습니다.

#### 전체 적인 예
```java
List<String> strings = List.of("i", "am", "a", "list", "of", "strings");

Stream<String> stream = strings.stream(); // strings의 stream 가져오기
Stream<String> limit = stream.limit(4); // 리턴 할 결과를 최대 4개로 설정
long result = limit.count(); // count 라는 최종 연산 호출
System.out.println(result);

// 이 코드는 `strings` 리스트에서 소문자로 변환했을 때 "h"로 시작하는 문자열들만 필터링하여 새로운 리스트로 반환합니다.
Stream<String> stream = strings.stream().filter(e
												->e.toLowerCase()
												.startswitch("h"))
												.collect(Collectors.toList());
```

## 13장
### 예외처리
```java
public void takeRisk() throws BadException, NiceException {
	if(abandonAllHope){
		throw new BedException(); // 예외 발생 시 새로운 객체를 만들고 던진다.
	}
}



public static void main(String[] args){
	try{
		anObject.taksRisk();
	}catch(BadException e){ // 해당 부분에서 던져진 예외를 받아서 처리한다. 
		e.printStackTrace(); // 문제가 생기는 코드를 알려준다.
	}catch(NiceException ex){
		// 복수의 예외를 던졌다면 해당 예외도 잡을 수 있습니다.
	}finally{
		// 예외 발생 여부와 상관없이 무조건 실행하는 코드입니다.
	}

// 상속의 경우에는 (작은것)자식 ~ (큰것)부모로 catch문을 작성해야 한다
// 위의 구조는 항상 지켜져야 한다.
// try, finally만 사용할 수 있지만 해당경우에는 실행하는 메서드에서 예외를 다른 곳으로 던져 주어야 합니다.
}
```

## 14장
### 직렬화된 객체를 파일에 저장하는 방법
```java
// 파일을 생성하거나 불러옵니다.
FileOutputStream fileStream = new FileOutputStream("MyGame.ser");
// 해당하는 파일에 연결해서 작업을 시작합니다.
ObjectOutputStream os = new ObjectOutputStream(fileStream);

// 객체를 저장 합니다.
os.writeObject(charactorOne); 
os.writeObject(charactorTwo); 
os.writeObject(charactorThree);

// fileStream을 포함하여 자동으로 닫힙니다. 스트림 최종연산 부분
os.close();


// 먼저 객체를 저장하려고 하면 해당하는 객체를 직렬화를 진행해 주어야 합니다.
public class Pond implements Serializable { // + implements Serializable
	// 직렬화 하는 과정에서 어떤 인스턴스를 건너뛰고 싶다면?
	transient String currntID; // + transient
} 
```

### 역직렬화 하여 객체에 저장하는 방법
```java
// 파일을 불러오는 부분입니다. 파일이 없으면 예외가 발생합니다. 
FileInputStream fileStream = new FileOutputStream("MyGame.ser");
// 해당하는 파일에 연결해서 작업을 시작합니다.
ObjectIutputStream os = new ObjectOutputStream(fileStream);

// 파일에서 객체 단위로 순서대로 읽어와서 객체에 저장합니다.
Object one = os.readObject(); 
Object two = os.readObject(); 
Object three = os.readObject();

// 파일에 저장된 양 보다 더 가져오려고 하면 예외가 발생한다.
Object four = os.readObject(); // 예외가 발생합니다.

// Object 객체를 다시 원래의 객체에 맞게 캐스트 합니다.
GameCharacter elf = (GameCharacter) one;
GameCharacter troll = (GameCharacter) two;
GameCharacter magician = (GameCharacter) three;

// fileStream을 포함하여 자동으로 닫힙니다. 스트림 최종연산 부분
os.close();
```


### 텍스트 파일을 읽는 방법1
```java
class ReadAFile{
	public static void main(Stringp[] args){
		File f = new File("myFile.txt");
		File dir = new File("myFile.txt");
		dir.mkdir();
		
		if(dir.isDirectory()){
			String[] dirContents = dir.List();
			for(String dirContent : dirContents){
				System.out.println(dirContent);
			}
		}
		
		boolean isDeleted = f.delete(); // 삭제 성공시 true
	}

}
```

### 텍스트 파일을 읽는 방법2
```java
class ReadAFile{
	public static void main(Stringp[] args){
		try{
			File myFile = new File("myFile.txt");
			FileReader fileReader = new FileReader(myFile);
			
			BufferedReader reader = new BufferedReader(fileReader);


			 String line;
			 While((line = reader,readLine()) != null ){
				 Syste.out.println(line);
			 }
			 reader.close();
		}catch(IOException e){
			e.printStackTrace();
		}
	}
}
```
# 핵심정리
- 9장
	- 인스턴스 변수는 그 변수가 들어 있는 객체 안에 (힙 안에) 저장됩니다.
	- 인스턴스 변수가 객체에 대한 레퍼런스인 경우에는 레퍼런스와 객체가 모드 힙에 저장됩니다.
	- 어떤 클래스 타입에 대해 new 키워드를 사용할 때 실행되는 코드를 생성자라고 합니다.
	- 생성자명은 반드시 클래스 명과 같아야 하며 리턴 타입은 없어야 합니다.
	- 생성자를 이용해서 생성되는 객체의 상태(인스턴스 변수)를 초기화 할 수 있습니다.
	- 클래스에 생성자가 없으면 컴파일러에서 기본 생성자를 만듭니다.
	- 기본 생성자는 언제나 인자가 없는 생성자 입니다.
	- 클래스를 만들 때 생성자를 만들면 (어떤 종류의 생성자를 만들어도) 컴파일러에서 기본생성자를 만들어 주지 않습니다.
	- 인자가 없는 생성자를 만들고 싶은데, 인자가 있는 생성자가 따로 있다면 인자가 없는 생성자도 손수 만들어야 합니다.
	- 가능하면 프로그래어머가 제대로된 객체를 만들 수 있게 인자가 없는 생성자도 만드는 것이 좋습니다. 그런 경우에는 기본값을 지정 해야겠죠?
	- 생성자 오버로딩을 활용하면 클래스에 두 개 이상의 생성자를 만들 수 있습니다.
	- 오버로드 된 생성자들의 인자 목록은 반드시 서로 달라야 합니다.
	- 인자 목록이 똑같은 생성자가 두개 이상 있을 수 없습니다. 인자 목록을 따질 때는 순서와 인자의 타입을 모두 따집니다.
	- 프로그래머가 직접 기본값을 지정하지 않아도 인스턴스 변수에는 자동으로 기본값이 지정됩니다. 원시 타입의 기본값은 0/0.0/false 고 객체에 대한 레퍼런스의 기본값은 null 입니다.
	- 상속된 자식 객체에서 부모 객체의 생성자를 실행할때 super() 를 호출 하게 됩니다. 만약 코드가 없다면 컴파일러가 자동으로 추가해 줍니다. 다만 컴파일러가 추가한 super()는 항상 기본생성자를 호출하게 됩니다. 인자가 있는 생성자를 호출하기 위해서는 직접 super(인자)를 작성해 주어야 합니다. super() 구분 추가 시 항상 생성자의 가장 처음에 위치해야합니다.

- 10장
	- 정적메서드는 객체 레퍼런스 변수 대신 클래스 명을 써서 호출 합니다.
	- 정적 메서드는 힙에 그 메서드가 들어있는 클래스의 인스턴스가 없어도 호출할 수 있습니다.
	- 특정 인스턴스 변숫값에 의존하지 않는유틸리티 메서드는 정적 메서드로 만드는 것이 좋습니다.
	- 정적 메서드에서는 특정 인스턴스와는 연관되지 않았으므로 어떤 인스턴스 변숫값도 사용할 수 없습니다.
	- 어떤 인스턴스에 들어있는 인스턴스 변숫값을 사용해야 할지 결정할 수 없기 때문입니다.
	- 정적 메서드가 아닌 메서드는 보통 인스턴스 변수 상태와 연관되어 있으므로 정적 메서드에는 정적 메서드가 아닌 메서드를 사용할 수 없습니다.
	- 정적 메서드만 들어있는 클래스가 있다면 그 클래스의 인스턴스를 만들 필요가 없으므로 그 생성자를  private로 지정하는 것이 좋습니다.
	- 정적 변수는 해당 클래스에 속하는 모든 객체에서 공유하는 변수 입니다. 인스턴스 변수는 각 객체마다 사본이 하나씩 있지만 정적 변수는 한클래스에 복사본이 하나밖에 없습니다.
	- 정적 메서드에서도 정적 변수를 사용할 수 있습니다.
	- 자바에서 상수를 만들 때는 변수에 static 과 final로 지정하면 됩니다.
	- final로 지정한 정적 변수는 변수를 선언할 때 또는 정적 초기화 부분에서 반드시 값을 대입해야 합니다.
	- 상수의 이름은 전부 대문자를 사용하고 각 단어 사이에는 _ 을 넣어 줍니다.
	- final로 지정한 변숫값은 값을 한 번 대입하면 바꿀 수 없습니다.
	- fianl인스턴스 변숫값은 선언할 때 또는 생성자에서 대입해야 합니다.
	- final메서드는 오버라이드 할 수 없습니다.
	- final클래스는 확장할 수 없습니다(하위 클래스를 만들 수 없습니다.).

- 14 장
	- 객체를 직렬화 하면 객체의 상태를 저장할 수 있습니다.
	- 객체를 직렬화 하려면 ObjectOutputStream이 필요합니다.
	- 스트림에는 연결 스트림과 연쇄 스트림이 있습니다.
	- 연결 스트림은 출발지나 목적지에 대한 연결을 나타냅니다.
	- 연쇄 스트림은 출발지 또는 목적지에 연결할 수 없기 때문에 반드시 연쇄 스트림 또는 다른 스트림에 연쇄 되어야 합니다.
	- 객체를 직렬화 해서 파일로 저장하고 싶다면 FileOutputStream 을 만들고 그 스트림에 ObjectOutputStream을 연쇄 시키면 됩니다.
	- 객체를 직렬화 할 때는 ObjectOutputStream의 writeObject(the Object)메서드를 호출 하면 됩니다. FileOutputStream 에 있는 메서드는 호출할 필요가 없습니다.
	- Serializable 인터페이스를 구현한 객체만 직렬화 할 수 있습니다. 어떤 클래스의 상위 클래스 중에 Serializable 을 구현하는 클래스가 있다면 선언할 때 implements Serializable이라고 쓰지 않아도 자동으로 직렬화 할 수 있는 클래스가 됩니다.
	- 객체가 직렬화 되면 그 객체와 연관된 모든 객체가 직렬화 됩니다. 즉 직렬화 된 객체의 인스턴스 변수에 의해 참조된 객체들도 모두 직렬화되고 그 객체들에서 참조하는 객체들도 모드 직렬화되고 ,, 이런식으로 연관된 모든 것들이 직렬화 됩니다.
	- 연관된 객체 중에서 직렬화할 수 없는 것이 하나라도 있으면 직렬화 과정에서 그 인스턴스 변수를 건너뛰지 않는 이상 실행중에 예외가 던져집니다.
	- 직렬화할 때 어떤 객체를 건너뛰고 싶다면 transient 키워드를 사용하면 됩니다. 그 변수는 나중에 복구될 때 null 또는 기본값을 할당 받게 됩니다.
	- 역직렬화를 할 때는 그 JVM에서 해당 객체와 연관된 모든 객체의 클래스를 사용할 수 있어야만 합니다.
	- 객체를 읽을때는 처음에 객체를 저장한 것과 같은 순서로 읽어오게 됩니다.
	- readObject 의 리턴 타입은 Object 이므로 역직렬화 과정에서 원래 타입으로 캐스트  해야 합니다.
	- 정적변수는 직렬화 되지 않습니다. 정적 변숫값은 한 타입에 속하는 모든 객체들이 클래스에 들어 있는 단 한 개뿐인 값을 공유하기 때문에 특정 객체 상태의 일부로 저장할 이우가 전혀 없습니다.
	- Serializable 을 구현하는 클래스가 나중에 바뀔 수 있다면 그 클래스에 static final long SerialVersionUID를 집어넣어 주세요. 그 클래스에 있는 직렬화된 변수가 바뀌면 이 버전 ID도 바뀌어야 합니다.