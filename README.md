# Algorithms
#include<bits/stdc++.h>
using namespace std;
#define usg "\n"

int main() {
	string str;
	cin>>str;//ababba
	str+="$";
	int n=size(str);//str.size()
    vector<int> c(n),p(n);
    //for(int i=0;i<n;i++) cout<<str[i]<<" "<<i<<usg;
        /***1)Take the pair as input char and int ,equivalence class of each suffix,
        sequences of sufixces is called suffix array***/
   {
       //k=0 iteration
    vector<pair<char,int>>a(n);//str="ababba$"
    for(int i=0;i<n;i++)
        a[i]={str[i],i};
        //  cout<<a[i].first<<" "<<a[i].second<<usg;}
        sort(a.begin(),a.end());//example str "$aaabbb"
        for(int i=0;i<n;i++)  
            p[i]=a[i].second;//p(6)= [6,0,2,5,1,3,4] array of sorted indexes of given string
        c[p[0]]=0;
            for(int i=1;i<n;i++)// a(6)={($,6),(a,0),(a,2),(a,5),(b,1),(b,3),(b,4)}
            {
            if(a[i].first==a[i-1].first)  //equivalence classes of given str in first iteration
            c[p[i]]=c[p[i-1]];            //by comparing char of string
            else c[p[i]]=c[p[i-1]]+1;     //c(6)={1,2,1,2,2,1,0} , {6,0,2,5,1,3,4
            }                             //                        $,a,a,a,b,b,b}
    }
	//2)iterate k->k+1 by comapring previous equivalence classes
	int k=0;
	while((1<<k) < n)
    {
	    vector<pair<pair<int,int>,int>> a(n);
	    for(int i=0;i<n;i++)
	    {
	        a[i]={{c[i],c[(i+ 1<<k)%n]},i};//c[i]=leftside,c[i+..k]=right side of string
	       // cout<<"("<<a[i].first.first<<" "<<a[i].first.second<<")"<<" "<<a[i].second<<usg;
	    }
	    sort(a.begin(),a.end());
	    for(int i=1;i<n;i++)
	       p[i]=a[i].second; 
        c[p[0]]=0;
        for(int i=1;i<n;i++)
        {
            if(a[i].first==a[i-1].first)  
            c[p[i]]=c[p[i-1]];            
            else c[p[i]]=c[p[i-1]]+1;    
        }
        
       k++; 
	}
	       for(int i=0;i<n;i++)
	        {
	        cout<<p[i]<<" "<<str.substr(p[i],n-p[i])<<endl;
	        }
//	cout<<n;
	return 0;
}
