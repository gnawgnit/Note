## 推箱子代码

```c
#include<stdio.h>
#include<windows.h>
#include<stdlib.h>
#include<conio.h>
#define GameLelve 5

//地图
//0:空地 1:墙壁 3:箱子目的地 4:箱子
//6:人   7:箱子到达目的地 9：人站在目的地
void Drawmap(void);//打印地图
struct POINT
{
	LONG x;
	LONG y;
};//, *PPOINT, NEAR *NPPOINT, FAR *LNPPOINT;
POINT GetGamerpostion(void);//获取玩家坐标
void Up(void);//往上
void Down(void);//往下
void Left(void);//往左
void Right(void);//往右
int GetSpareBox(void);//获取剩余箱子数
void SetColor(int ncolor);//设置颜色
int g_map[GameLelve][10][12]=
{
	{
		{1,1,1,1,1,0,0,0,0,0,0,0},
		{1,0,0,0,1,0,1,1,1,0,0,0},
		{1,0,4,0,1,0,1,1,1,1,1,1},
		{1,0,4,6,1,0,1,0,0,0,3,1},
		{1,1,1,4,1,1,1,0,0,0,3,1},
		{1,1,1,0,0,0,0,0,0,0,3,1},
		{0,1,0,0,0,1,0,0,0,0,0,1},
		{0,1,0,0,0,1,0,0,0,0,0,1},
		{0,1,0,0,0,1,1,1,1,1,1,1},
		{0,1,1,1,1,1,0,0,0,0,0,0},
	},
	{
		{0,1,1,1,1,0,0,0,0,0,0,0},
		{0,1,1,1,1,1,1,1,1,0,0,0},
		{0,1,0,0,0,0,1,1,1,1,1,1},
		{1,1,4,1,1,0,1,1,0,0,0,1},
		{1,0,6,0,1,0,0,1,0,0,0,1},
		{1,0,0,1,1,1,0,0,0,0,0,1},
		{1,0,0,0,4,0,0,4,0,0,0,1},
		{1,0,3,3,1,0,4,0,0,0,1,1},
		{1,1,3,3,1,0,0,0,1,1,1,0},
		{0,1,1,1,1,1,1,1,1,1,1,0}
	},
	{
		{0,1,1,1,1,1,1,0,0,0,0,0},
		{0,1,6,0,0,0,1,1,1,0,0,0},
		{1,1,0,1,1,4,0,3,1,1,0,0},
		{1,0,0,0,4,0,4,3,3,1,0,0},
		{1,1,0,4,0,4,0,3,3,1,0,0},
		{0,1,0,0,1,1,1,1,1,1,0,0},
		{0,1,1,1,1,0,0,0,0,0,0,0},
		{0,0,0,0,0,0,0,0,0,0,0,0},
		{0,0,0,0,0,0,0,0,0,0,0,0},
		{0,0,0,0,0,0,0,0,0,0,0,0}
	},
	{
		{1,1,1,1,1,0,0,0,0,0,0,0},
		{1,0,0,0,1,1,0,0,0,0,0,0},
		{1,0,4,0,0,1,0,0,0,0,0,0},
		{1,1,0,4,0,1,1,1,1,0,0,0},
		{0,1,1,1,6,3,0,0,1,0,0,0},
		{0,0,1,0,0,3,1,0,1,0,0,0},
		{0,0,1,0,0,0,0,0,1,0,0,0},
		{0,0,1,1,1,1,1,1,1,0,0,0},
		{0,0,0,0,0,0,0,0,0,0,0,0},
		{0,0,0,0,0,0,0,0,0,0,0,0}
	},
	{
		{0,0,1,1,1,1,1,1,1,0,0,0},
		{0,0,1,0,6,3,3,3,1,0,0,0},
		{0,0,1,0,0,0,1,1,1,1,0,0},
		{0,1,1,1,4,0,0,0,0,1,0,0},
		{0,1,0,0,0,1,4,1,0,1,0,0},
		{0,1,0,4,0,1,0,0,0,1,0,0},
		{0,1,0,0,0,1,1,1,1,1,0,0},
		{0,1,1,1,1,1,0,0,0,0,0,0},
		{0,0,0,0,0,0,0,0,0,0,0,0},
		{0,0,0,0,0,0,0,0,0,0,0,0}
	}
	
};
int g_nCurrentLevel = 0;//当前关卡
int main(void)
{
	
	//设置标题
	SetConsoleTitle("推箱子");
	//设置大小
	system("mode con cols=54 lines=12");
	while(1)
	{
		
		//获取剩余箱子数
		if(GetSpareBox() == 0)
		{
			g_nCurrentLevel++;
		}
		//关卡结束
		if(g_nCurrentLevel == GameLelve)
		{
			system("cls");
			printf("恭喜通关！");
			break;
		}
		system("cls");
		Drawmap();
		char ch = getch();
		switch(ch)
		{
			case 'w':case 72://向上移动
			Up();
			break;
			case 's':case 80://向下
			Down();
			break;
			case 'a':case 75://向左
			Left();
			break;
			case 'd':case 77://向右
			Right();
			break;
			
		}

		
	}
	return 0;
}
//设置颜色
void SetColor(int ncolor)
{
	HANDLE hConsole = GetStdHandle(STD_ERROR_HANDLE);
	SetConsoleTextAttribute(hConsole, ncolor);
}
//打印地图
void Drawmap(void)
{
	int i, j;
		for(i=0;i<10;i++)
		{
			for(j=0;j<12;j++)
			{
				switch(g_map[g_nCurrentLevel][i][j])
				{
					case 0://空地
					printf("  ");
					break;
					case 1://墙壁
					SetColor(FOREGROUND_RED | FOREGROUND_INTENSITY);
					printf("■");
					break;
					case 3://目的地
					SetColor(FOREGROUND_GREEN | FOREGROUND_INTENSITY);
					printf("☆");
					break;
					case 4://箱子
					SetColor(FOREGROUND_RED | FOREGROUND_BLUE | FOREGROUND_INTENSITY);
					printf("□");
					break;
					case 6://人
					SetColor(FOREGROUND_BLUE | FOREGROUND_INTENSITY);
					printf("♀");
					break;
					case 7://箱子在目的地
					SetColor(FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_INTENSITY);
					printf("★");
					break;
					case 9://人在目的地
					SetColor(FOREGROUND_RED | FOREGROUND_INTENSITY);
					printf("♀");
					break;
				}
			}
			printf("\n");
		}
}
//往上
void Up(void)
{
	POINT pos = GetGamerpostion();
	
	//1.人的前面是空地
	if(g_map[g_nCurrentLevel][pos.x-1][pos.y] == 0)
	{
		g_map[g_nCurrentLevel][pos.x-1][pos.y] = 6;//空地改为人
		//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
	}

	
	//2.人的前面是目的地
	if(g_map[g_nCurrentLevel][pos.x-1][pos.y] == 3)
	{
		g_map[g_nCurrentLevel][pos.x-1][pos.y] = 9;//人站在目的地
		//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
	}
	//3.人的前面箱子
	if(g_map[g_nCurrentLevel][pos.x-1][pos.y] == 4)
	{
		//a.箱子前面是目的地
		if(g_map[g_nCurrentLevel][pos.x-2][pos.y] == 3)
		{
			g_map[g_nCurrentLevel][pos.x-2][pos.y] = 7;
			g_map[g_nCurrentLevel][pos.x-1][pos.y] = 6;
			//原来的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
		//b.箱子前面是空地
		if(g_map[g_nCurrentLevel][pos.x-2][pos.y] == 0)
		{
			g_map[g_nCurrentLevel][pos.x-2][pos.y] = 4;
			g_map[g_nCurrentLevel][pos.x-1][pos.y] = 6;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
	}
	//4.人的前面是箱子和目的地的重合
	if(g_map[g_nCurrentLevel][pos.x-1][pos.y] == 7)
	{
		//a.箱子前面是空地
		if(g_map[g_nCurrentLevel][pos.x-2][pos.y] == 0)
		{
			g_map[g_nCurrentLevel][pos.x-2][pos.y] = 4;
			g_map[g_nCurrentLevel][pos.x-1][pos.y] = 9;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
			
		}			
		//b.箱子前面是目的地
		if(g_map[g_nCurrentLevel][pos.x-2][pos.y] == 3)
		{
			g_map[g_nCurrentLevel][pos.x-2][pos.y] = 7;
			g_map[g_nCurrentLevel][pos.x-1][pos.y] = 9;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
	}
}
//往下
void Down(void)
{
	POINT pos = GetGamerpostion();
	
	//1.人的前面是空地
	if(g_map[g_nCurrentLevel][pos.x+1][pos.y] == 0)
	{
		g_map[g_nCurrentLevel][pos.x+1][pos.y] = 6;//空地改为人
		//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
	}

	
	//2.人的前面是目的地
	if(g_map[g_nCurrentLevel][pos.x+1][pos.y] == 3)
	{
		g_map[g_nCurrentLevel][pos.x+1][pos.y] = 9;//人站在目的地
		//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
	}
	//3.人的前面箱子
	if(g_map[g_nCurrentLevel][pos.x+1][pos.y] == 4)
	{
		//a.箱子前面是目的地
		if(g_map[g_nCurrentLevel][pos.x+2][pos.y] == 3)
		{
			g_map[g_nCurrentLevel][pos.x+2][pos.y] = 7;
			g_map[g_nCurrentLevel][pos.x+1][pos.y] = 6;
			//原来的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
		//b.箱子前面是空地
		if(g_map[g_nCurrentLevel][pos.x+2][pos.y] == 0)
		{
			g_map[g_nCurrentLevel][pos.x+2][pos.y] = 4;
			g_map[g_nCurrentLevel][pos.x+1][pos.y] = 6;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
	}
	//4.人的前面是箱子和目的地的重合
	if(g_map[g_nCurrentLevel][pos.x+1][pos.y] == 7)
	{
		//a.箱子前面是空地
		if(g_map[g_nCurrentLevel][pos.x+2][pos.y] == 0)
		{
			g_map[g_nCurrentLevel][pos.x+2][pos.y] = 4;
			g_map[g_nCurrentLevel][pos.x+1][pos.y] = 9;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
			
		}			
		//b.箱子前面是目的地
		if(g_map[g_nCurrentLevel][pos.x+2][pos.y] == 3)
		{
			g_map[g_nCurrentLevel][pos.x+2][pos.y] = 7;
			g_map[g_nCurrentLevel][pos.x+1][pos.y] = 9;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
	}
}
//往左
void Left(void)
{
	POINT pos = GetGamerpostion();
	
	//1.人的前面是空地
	if(g_map[g_nCurrentLevel][pos.x][pos.y-1] == 0)
	{
		g_map[g_nCurrentLevel][pos.x][pos.y-1] = 6;//空地改为人
		//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
	}

	
	//2.人的前面是目的地
	if(g_map[g_nCurrentLevel][pos.x][pos.y-1] == 3)
	{
		g_map[g_nCurrentLevel][pos.x][pos.y-1] = 9;//人站在目的地
		//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
	}
	//3.人的前面箱子
	if(g_map[g_nCurrentLevel][pos.x][pos.y-1] == 4)
	{
		//a.箱子前面是目的地
		if(g_map[g_nCurrentLevel][pos.x][pos.y-2] == 3)
		{
			g_map[g_nCurrentLevel][pos.x][pos.y-2] = 7;
			g_map[g_nCurrentLevel][pos.x][pos.y-1] = 6;
			//原来的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
		//b.箱子前面是空地
		if(g_map[g_nCurrentLevel][pos.x][pos.y-2] == 0)
		{
			g_map[g_nCurrentLevel][pos.x][pos.y-2] = 4;
			g_map[g_nCurrentLevel][pos.x][pos.y-1] = 6;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
	}
	//4.人的前面是箱子和目的地的重合
	if(g_map[g_nCurrentLevel][pos.x][pos.y-1] == 7)
	{
		//a.箱子前面是空地
		if(g_map[g_nCurrentLevel][pos.x][pos.y-2] == 0)
		{
			g_map[g_nCurrentLevel][pos.x][pos.y-2] = 4;
			g_map[g_nCurrentLevel][pos.x][pos.y-1] = 9;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
			
		}			
		//b.箱子前面是目的地
		if(g_map[g_nCurrentLevel][pos.x][pos.y-2] == 3)
		{
			g_map[g_nCurrentLevel][pos.x][pos.y-2] = 7;
			g_map[g_nCurrentLevel][pos.x][pos.y-1] = 9;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
	}
}
//往右
void Right(void)
{
	POINT pos = GetGamerpostion();
	
	//1.人的前面是空地
	if(g_map[g_nCurrentLevel][pos.x][pos.y+1] == 0)
	{
		g_map[g_nCurrentLevel][pos.x][pos.y+1] = 6;//空地改为人
		//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
	}

	
	//2.人的前面是目的地
	if(g_map[g_nCurrentLevel][pos.x][pos.y+1] == 3)
	{
		g_map[g_nCurrentLevel][pos.x][pos.y+1] = 9;//人站在目的地
		//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
	}
	//3.人的前面箱子
	if(g_map[g_nCurrentLevel][pos.x][pos.y+1] == 4)
	{
		//a.箱子前面是目的地
		if(g_map[g_nCurrentLevel][pos.x][pos.y+2] == 3)
		{
			g_map[g_nCurrentLevel][pos.x][pos.y+2] = 7;
			g_map[g_nCurrentLevel][pos.x][pos.y+1] = 6;
			//原来的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
		//b.箱子前面是空地
		if(g_map[g_nCurrentLevel][pos.x][pos.y+2] == 0)
		{
			g_map[g_nCurrentLevel][pos.x][pos.y+2] = 4;
			g_map[g_nCurrentLevel][pos.x][pos.y+1] = 6;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
	}
	//4.人的前面是箱子和目的地的重合
	if(g_map[g_nCurrentLevel][pos.x][pos.y+1] == 7)
	{
		//a.箱子前面是空地
		if(g_map[g_nCurrentLevel][pos.x][pos.y+2] == 0)
		{
			g_map[g_nCurrentLevel][pos.x][pos.y+2] = 4;
			g_map[g_nCurrentLevel][pos.x][pos.y+1] = 9;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
			
		}			
		//b.箱子前面是目的地
		if(g_map[g_nCurrentLevel][pos.x][pos.y+2] == 3)
		{
			g_map[g_nCurrentLevel][pos.x][pos.y+2] = 7;
			g_map[g_nCurrentLevel][pos.x][pos.y+1] = 9;
			//原来人的位置还原
		if(g_map[g_nCurrentLevel][pos.x][pos.y] == 9)
			g_map[g_nCurrentLevel][pos.x][pos.y] = 3;
		else
			g_map[g_nCurrentLevel][pos.x][pos.y] = 0;
		}
	}
}
//获取玩家坐标
POINT GetGamerpostion(void)
{
	int i, j;
	POINT pos = {-1,-1};
	for(i=0;i<10;i++)
	{
		for(j=0;j<12;j++)
		{
			if(g_map[g_nCurrentLevel][i][j]==6||g_map[g_nCurrentLevel][i][j]==9)
			{
				pos.x = i;
				pos.y = j;
				return pos;
			}
		}
	}
	return pos;
}
//获取剩余箱子数
int GetSpareBox(void)
{
	int i, j,count = 0;
	for(i=0;i<10;i++)
	{
		for(j=0;j<12;j++)
		{
			if(g_map[g_nCurrentLevel][i][j]== 4 )
				count++;
		}
	}
	return count;
}
```

