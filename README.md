# ■ 신체검사 리스트 ■

## [시력의 분포를 구하기 위하여 0.0 부터 0.1 단위로 2.0 까지 21개의 칸을 만든다.]
```java
static final int VMAX = 21; // 시력의 분포(0.0부터 0.1 단위로 21개) // 정적 상수 필드
```
## [신체정보]
* ### String name, int height, double vision 이라는 멤버 변수를 선언한다.
* ### 생성자를 이용하여 멤버변수 안에 값을 넣어주는데, 매개변수로 가져온 Type과 변수명이 같을 경우 멤버변수와 매개변수를 구분하기 위하여 this를 사용한다.
```java
static class PhysData{
   String name;	   // 이름
   int    height;  // 키
   double vision;  // 시력

       // --- 생성자(constructor) --- //
   PhysData(String name, int height, double vision) {
       this.name = name;
       this.height = height;
       this.vision = vision;
  }
}
```
## [키의 평균]
* ### 신체정보를 매개변수로 받아와서 신체정보 수 만큼 키를 sum에 더한다.
* ### 평균을 구하는 식은 sum / (신체정보 수) 를 해주면 평균값을 리턴해준다.
```java
// --- 키의 평균값을 구함 --- //
static double aveHeight(PhysData[] dat) {
    double sum = 0;
		
    for (int i = 0; i < dat.length; i++) {
         sum += dat[i].height;
    }
    return sum / dat.length;
}
```
## [시력의 분포]
* ### 신체정보 중에 그 시력에 해당하는 사람이 몇명이 있나를 검사하는 코드이다.
* ### 신체정보, VMAX값 크기의 dist배열을 매개변수로 받아서 시력이 0.0보다 크거나 작고 시력이 VMAX / 10.0 보다 작거나 같을 때 dist배열 안에 +1 을 해 준다.
```java
// --- 시력의 분포를 구함 --- //
static void distVision(PhysData[] dat, int[] dist) {
    for (int j = 0; j < 21; j++) dist[j] = 0; {
         for(int i = 0; i < dat.length; i++) {
            if(dat[i].vision >= 0.0 && dat[i].vision <= VMAX / 10.0) {
                dist[(int)(dat[i].vision * 10)]++;
            }
         }
     }
}
```






## Java Code
```java
class PhysicalExamination {
	static final int VMAX = 21; // 시력의 분포(0.0부터 0.1 단위로 21개) // 정적 상수 필드

	static class PhysData {
		String name; // 이름
		int height; // 키
		double vision; // 시력

		// --- 생성자(constructor) --- //
		PhysData(String name, int height, double vision) {
			this.name = name;
			this.height = height;
			this.vision = vision;
		}
	}

	// --- 키의 평균값을 구함 --- //
	static double aveHeight(PhysData[] dat) {
		double sum = 0;

		for (int i = 0; i < dat.length; i++) {
			sum += dat[i].height;
		}
		return sum / dat.length;
	}

	// --- 시력의 분포를 구함 --- //
	static void distVision(PhysData[] dat, int[] dist) {
		for (int j = 0; j < 21; j++) {
			dist[j] = 0;
		}
		for (int i = 0; i < dat.length; i++) {
			if (dat[i].vision >= 0.0 && dat[i].vision <= VMAX / 10.0) {
				dist[(int) (dat[i].vision * 10)]++;
			}
		}
	}

	public static void main(String[] args) {

		PhysData[] x = { 
				new PhysData("강민하", 162, 0.3), 
				new PhysData("김찬우", 173, 0.7), 
				new PhysData("박준서", 175, 2.0),
				new PhysData("유서범", 171, 1.5), 
				new PhysData("이수연", 168, 0.4), 
				new PhysData("장경오", 174, 1.2),
				new PhysData("황지안", 169, 0.8), };
		int[] vdist = new int[VMAX]; // 시력의 분포

		System.out.println("■ 신체검사 리스트 ■");
		System.out.println(" 이름    키   시력");
		System.out.println("---------------");

		for (int i = 0; i < x.length; i++) {
			System.out.printf("%-6s%3d%5.1f\n", x[i].name, x[i].height, x[i].vision);
		}
		System.out.printf("\n평균 키: %5.1fcm\n", aveHeight(x));

		distVision(x, vdist); // 시력의 분포를 구함
		System.out.println("\n시력 분포");
		for (int i = 0; i < VMAX; i++) {
			System.out.printf("%3.1f~: %2d명\n", i / 10.0, vdist[i]);
		}
	}

}
```
