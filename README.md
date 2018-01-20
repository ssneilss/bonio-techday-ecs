## AWS ECS基本概念與範例

### ECS Infrastructure
![image](https://user-images.githubusercontent.com/7845386/35181523-34e395bc-fdfe-11e7-8a79-3746717b7de8.png)

### ECS Components - Image > Task > Service > Cluster
![image](https://user-images.githubusercontent.com/7845386/35181600-edd9cb94-fdff-11e7-8382-cb1dc4acdacc.png)

### Example1 - 部署一個NodeJS Web Application

### Example2 - 部署一個使用NGINX做反向代理的NodeJS Web Application

### Example3 - 如何使用Jenkins ECS Slaves Plugin增加CI/CD效率

## AWS ECS vs AWS Lambda

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
