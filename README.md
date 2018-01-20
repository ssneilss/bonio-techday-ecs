## AWS ECS基本概念與範例

### ECS Infrastructure
![image](https://user-images.githubusercontent.com/7845386/35181523-34e395bc-fdfe-11e7-8a79-3746717b7de8.png)

### ECS Components - Image > Task > Service > Cluster
![image](https://user-images.githubusercontent.com/7845386/35181600-edd9cb94-fdff-11e7-8382-cb1dc4acdacc.png)

### Example1 - 部署一個NodeJS Web Application

### Example2 - 部署一個使用NGINX做反向代理的NodeJS Web Application

### Example3 - 如何使用Jenkins ECS Slaves Plugin增加CI/CD效率

## AWS ECS vs AWS Lambda
| Services | Lambda | ECS |
| --- | --- | --- |
| Languages Support | Node.js (JavaScript)、Python、Java (與 Java 8 相容) 和 C# (.NET Core) | 不限 |
| Pricing | 每100ms為單位計費（不足則算100ms，通常較為便宜） | 以小時計費（同EC2，通常較為昂貴） |
| Networking | 沒有Public IP、無法ssh | 有Public IP，可以ssh（同EC2） |
| Timeout | （重要）最多5分鐘 | 無限制 |
| Environment | 較簡單，但比較沒有自由安裝套件等的彈性 ｜ 較複雜，但較有彈性 |
| Libraries / Dependencies | （重要）總共最多250MB(zip壓縮後) | 無限制 |
| Scale | 全受管，不需要特別設定 | 需要進行AutoScaling的設定 |
| Logging | 進到AWS CloudWatch集中管理 | 可以自行設定 |
| Summary | 較適合拿來做計算、與其他AWS服務的串接（e.g. DynamoDB） | 較適合拿來做Web Service | 

## AWS ECS Auto Scaling
### ![image](https://user-images.githubusercontent.com/7845386/35181647-c984f948-fe00-11e7-90b6-042f2c10a31e.png)
### Example4 - 錯誤示範：Cluster設定80%的Memory Utilization，t2 Large Instance，但每個Task的Memory Reservation為512MB...
| # of Tasks  | # of Container Instances  | Reserved Memory before | Memory needed | Reserved Memory after | What happens |
|---|---|---|---|---|---|
| 0	| 1	| 0% (0 MB) |	512 MB | 25% (512 MB)	| Task is scheduled
| 1	| 1	| 25% (512 MB) | 512 MB	| 50% (1024 MB) |	Task is scheduled
| 2	| 1	| 50% (1024 MB) |	512 MB | 75% (1536 MB) | Task is scheduled
| 3	| 1	| 75% (1536 MB) |	512 MB | | Task can’t be scheduled
### Rule of Thumb
`Threshold = (1 - max(Container Reservation) / Total Capacity of a Single Container Instance) * 100`

### Example5 - Fácil的部署實例
