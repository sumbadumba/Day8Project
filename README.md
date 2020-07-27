# Day8Project

//#include<stdio.h>
//
//
//#define OPTION_1 0x0000001
//#define OPTION_2 0x0000010
//#define OPTION_3 0x0000100
//
//#define SWAP_DATA(a,b) { (a)^=(b)^=(a)^=(b); }//매크로함수, 함수매크로라고 함.
//
//
//int main()
//{
//	//비트 연산자
//
//	unsigned char num1 = 1;//1바이트 이자 8비트이다.(char)형에 한 함.
//	//0000 0001
//	unsigned char num2 = 3;
//	//0000 0011
//
//	printf("%d\n", (num1 & num2));
//
//		//0000 0001
//		//&&&& &&&&
//		//0000 0011
//	//  = 0000 0001 ->결과
//
//	// oR로 연산을 하면 
//	// 0000 0011으로 된다.
//	printf("%d\n", (num1 | num2));
//
//	/*num1 &= num2;
//	
//	num1 |= num2;*/
//
//	//unsigned char optionFlag = OPTION_1 | OPTION_3;
//	//(요런식으로 쓴다)
//	//if(어떤 조건)
//	   //optionFlag |= OPTION_3;
//
//
//	printf("%d\n", num1 ^ num2);
//	//exclusive OR (서로 다른 값일 때만 true이다.) ' ^ '
//
//	SWAP_DATA(num1, num2);
//
//	printf("after swap num1 = %d\n", num1);
//	printf("after swap num2 = %d\n", num2);//절묘한 테크닉임다
//
//	//시프트 연산자
//
//	unsigned char num3 = 1;
//	printf("num3 = %u\n", num3);
//
//	unsigned char num4 = num3 << 1;
//	printf("num4 = %u\n", num4);
//
//	unsigned char num5 = num4 << 1;
//	printf("num5 = %u\n", num5);
//
//	unsigned char num6 = num3 << 2;
//	printf("num6 = %u\n", num6);
//
//	unsigned char num7 = num3 << 3;
//	printf("num7 = %u\n", num7);
//
//	unsigned char num8 = num7 >> 2;
//	printf("num8 = %u\n", num8);
//
//	unsigned char num9 = num7 >> 3;
//	printf("num9 = %u\n", num9);
//
//	unsigned char num11 = 3;//0000 0011
//	unsigned char num12 = 24;//0001 1000
//
//	printf("num11 = %u\n", num11 << 3);//24: 0001 1000
//	printf("num12 = %u\n", num12 >> 2);// 6:0000 0110
//
//	unsigned char num21 = 128;//1000 0000
//	unsigned char num22 = 0;
//	num22 = (num21 << 1);
//
//	printf("num22 = %u\n", num22);//넘치는 것은 입력이 안된다.(그래서 값이 0이다)
//
//	//Ram의 약자는 (random exese memory)
//	//shift가 되는 것이다.
//	// << , >> 두가지가 존재 비트를 좌,우측으로 보내세요.
//	//0000 0001 - <<
//	//00000 0001
//	//0000 0010 과정
//	//<<
//	//0000 0100
//
//
//	//1111 1111 = 255;
//
//}



//bingo.cpp


#include<stdio.h>
#include<time.h>
#include<math.h>
#include<stdlib.h>


//배열의 주소를 
void PrintArray(int * arr, int width,int height)//배열을 함수로 받을 때 pointer를 받는 방법이다. : int * arr
{//pointer에 주소를 넘긴 것이다.
	printf("\n");

	for (int i = 0; i < height; i++)
	{
		for (int j = 0; j < width; j++)
		{
			printf("%d\t", arr[i * 5 + j]);//인덱스 5부터 찍는다.그러니 총 5번 찍는거임.
			
		}
		printf("\n");
	}

}
int main()
{
	// 5X5
	int bingoCount = 0;
	const int numCount = 25;
	int arr[numCount];
	int bingoCountToWin = 5;
	bool bingo = false;

	//배열초기화
	for (int i = 0; i < numCount; i++)
	{
		arr[i] = i + 1;

	}
	//배열을 출력



	//랜덤씨드
	srand(time(NULL));

	//srand((unsigned int)time(NULL));

	//램덤과 스왑을 이용해서 마구 섞는다.
	//for (int i = 0; i < 100; i++)
	//{
	//	int rndIndex1 = rand() % numCount;// 0 ~ 24

	//	int rndIndex2 = rand() % numCount;// 0 ~ 24
	//	//스왑
	//	int temp = arr[rndIndex1];
	//	arr[rndIndex1] = arr[rndIndex2];
	//	arr[rndIndex2] = temp;

	//}
	//섞인 배열을 출력
	PrintArray(arr, 5, 5);



	bingoCount = 0;
	while (true)
	{
		int input = 0;
		printf("\n숫자를 입력하세요. ");
		scanf("%d", &input);// scanf의 input 은 &주소값을 받는다.

		PrintArray(arr, 5, 5);
		system("cls");

		for (int i = 0; i < numCount; i++)//입력된 숫자를 0으로 초기화 한다.
		{
			if (arr[i] == input)
			{
				arr[i] = 0;
			}
		}

		//for (int i = 0; i < 5; i++)
		//{
		//	for (int j = 0; j < 5; j++)
		//	{
		//		if (arr[i * 5 + j] != 0)
		//		{
		//			printf("%d\t", arr[i * 5 + j]);
		//		}
		//		else
		//			printf("# \t");//0으로 초기화 한 숫자를 #으로 만들어 버린다.
		//	}
		//	printf("\n");

		//}
		PrintArray(arr, 5, 5);

		for (int i = 0; i < 5; i++)
		{
			// 가로줄로 검사
			if (arr[i * 5 + 0] == 0
				&& arr[i * 5 + 1] == 0
				&& arr[i * 5 + 2] == 0
				&& arr[i * 5 + 3] == 0
				&& arr[i * 5 + 4] == 0)
			{
				bingoCount++;
			}
			// 세로줄 검사
			if (arr[i + 5 * 0] == 0
				&& arr[i + 5 * 1] == 0
				&& arr[i + 5 * 2] == 0
				&& arr[i + 5 * 3] == 0
				&& arr[i + 5 * 4] == 0)
			{
				bingoCount++;
			}
		}

		if (arr[0] == 0
			&& arr[6] == 0
			&& arr[12] == 0
			&& arr[18] == 0
			&& arr[24] == 0)
		{// \대각선 방향
			bingoCount++;
		}
		if (arr[4] == 0
			&& arr[8] == 0
			&& arr[12] == 0
			&& arr[16] == 0
			&& arr[20] == 0)
		{
			bingoCount++;
		}// /대각선 방향

		if (bingoCount >= bingoCountToWin)
		{
			bingo = true;
			printf("\n\n빙고에 당첨되셨습니다. \n");
		}

		if (bingo == true)
		{
			break;
		}

	}
	return 0;
}

//습관을 들여라 
//while(true)
//{

//}//while end

