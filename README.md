
#include<bits/stdc++.h>
using namespace std;

const int board_size = 9;
const int cell_size = 3;

int board[board_size][board_size];


bool check(int row,int col,int x){
	// check in row
	for(int pc=0;pc<board_size;pc++){
		if(pc!=col && board[row][pc]==x){
			return false;
		}
	}
	// check in col
	for(int pr=0;pr<board_size;pr++){
		if(pr!=row && board[pr][col]==x){
			return false;
		}
	}
	// check in square
	int ro = (row/cell_size)*cell_size;
	int co = (col/cell_size)*cell_size;
	for(int i = 0;i<cell_size;i++){
		for(int j =0;j<cell_size;j++){
			if(ro+i==row && co+j==col)continue;
			if(board[ro+i][co+j]==x)return false;
		}
	}
	return true;
}

int ans = 0;

void rec(int row,int col){
	if(col==board_size){
		rec(row+1,0);
		return;
	}
	if(row==board_size){
		// base case
		ans++;

		cout<<"Answer "<<ans<<endl;
		for(int i=0;i<board_size;i++){
			for(int j=0;j<board_size;j++){
				cout<<board[i][j]<<" ";
			}
			cout<<endl;
		}
		return;
	}

	if(board[row][col]==0){
		// we need to fill.
		for(int x=1;x<=board_size;x++){
			if(check(row,col,x)){
				board[row][col] = x;
				rec(row,col+1);
				board[row][col] = 0;
			}
		}

	}else{
		// pre-filled.
		if(check(row,col,board[row][col])){
			rec(row,col+1);
		}
	}
}

/*
3 0 6 5 0 8 4 0 0
5 2 0 0 0 0 0 0 0
0 8 7 0 0 0 0 3 1
0 0 3 0 1 0 0 8 0
9 0 0 8 6 3 0 0 5
0 5 0 0 9 0 6 0 0
1 3 0 0 0 0 2 5 0
0 0 0 0 0 0 0 7 4
0 0 5 2 0 6 3 0 0
*/



signed main(){
	ios_base::sync_with_stdio(0);
	cin.tie(0); cout.tie(0);

	for(int i=0;i<board_size;i++){
		for(int j=0;j<board_size;j++){
			cin>>board[i][j];
		}
	}
	rec(0,0);
	}
