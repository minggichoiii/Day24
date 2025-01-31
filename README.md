# Day24
# 입력 받기
N, S, M = map(int, input().split())
V = list(map(int, input().split()))

# dp 배열 초기화
# dp[i]는 i번째 곡까지 연주한 후 가능한 볼륨을 True로 표시
dp = [False] * (M + 1)
dp[S] = True  # 시작 볼륨은 S

# 각 곡에 대해서 가능한 볼륨을 계산
for i in range(N):
    next_dp = [False] * (M + 1)
    for vol in range(M + 1):
        if dp[vol]:  # 현재 볼륨이 가능하면
            # V[i]만큼 볼륨을 올릴 수 있을 때
            if vol + V[i] <= M:
                next_dp[vol + V[i]] = True
            # V[i]만큼 볼륨을 내릴 수 있을 때
            if vol - V[i] >= 0:
                next_dp[vol - V[i]] = True
    dp = next_dp

# 마지막 곡 연주 후 가능한 볼륨 중 최댓값 찾기
for vol in range(M, -1, -1):
    if dp[vol]:
        print(vol)
        break
else:
    print(-1)
