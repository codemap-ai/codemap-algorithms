#include <iostream>
#include <vector>

using namespace std;

int main() {
	vector<int> A(10);
	A[0] = 1, A[9] = 10;
	cout << A.size() << " " << A.front() << " " << A.back() << "\n";
	
	vector<vector<int>> B(10, vector<int>(20, 1));
	cout << B.size() << " " << B.front().size() << " " << B.back().size() << "\n";
	cout << B[0].size() << " " << B[0][0] << "\n";
}
