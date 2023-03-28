# in20_200306X
#include <iostream>
#include <vector>
#include <ctime>
#include <stack>
#include <iomanip>

using namespace std;


int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort_nonrecursive(vector<int>& arr, int low, int high) {
    stack<int> st;

    st.push(low);
    st.push(high);

    while (!st.empty()) {
        high = st.top();
        st.pop();
        low = st.top();
        st.pop();

        int pi = partition(arr, low, high);

        if (pi - 1 > low) {
            st.push(low);
            st.push(pi - 1);
        }

        if (pi + 1 < high) {
            st.push(pi + 1);
            st.push(high);
        }
    }
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}


int main() {
int sz;
    printf("Enter the size of array:");
    scanf("%d",&sz);

    std::vector<int> arr(sz);
    for(int i = 0; i < sz; i++) {
        arr[i] = rand() % 100; //Generate number between 0 to 99
    }
    

//    std::vector<int> vec(arr, arr + sz);

    int n = arr.size();
for (int i = 0; i< n ; i++){
    
    vector<int> new_arr(i+1);
    std::copy(arr.begin() + 0, arr.begin() + i+1, new_arr.begin());

    quickSort(new_arr, 0, i );
      for (int i = 0; i < new_arr.size(); i++) {
        std::cout << new_arr[i] << " " ;
    }
     std::cout << endl ;
     int k = new_arr.size();
int c=new_arr.size()%2;
   if(c==0){
       double median=(new_arr[k/2]+new_arr[k/2-1])/2.0;

       cout<<"median="<<fixed<<setprecision(1) << median<<endl;
   }
   else{
       double median=new_arr[k/2];

      cout<<"median="<<fixed<<setprecision(1) << median<<endl;
   } 


}


    return 0;
}
