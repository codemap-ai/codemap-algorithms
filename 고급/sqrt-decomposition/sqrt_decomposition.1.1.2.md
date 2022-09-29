// 입력
int n;
vector<int> a (n);

// preprocessing
int len = (int) sqrt (n + .0) + 1; // 블록의 크기임과 동시에 전체 블록의 개수이다
vector<int> b (len);
for (int i=0; i<n; ++i)
    b[i / len] += a[i];

// 쿼리를 처리하는 부분
for (;;) {
    int l, r;
  // 다음 쿼리에 대한 입력을 받는다.
    int sum = 0;
    for (int i=l; i<=r; )
        if (i % len == 0 && i + len - 1 <= r) {
            // 블록이 구간 [l, r]에 포함되는 경우
            sum += b[i / len];
            i += len;
        }
        else {
            sum += a[i];
            ++i;
        }
}
