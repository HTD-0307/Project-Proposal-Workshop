# Proposal: Hệ thống Giám sát Kho hàng Thông minh với IoT Sensors
# Thông Tin Sinh Viên Thực Tập
-  👨‍🎓 **Họ và Tên**: Huỳnh Thành Đô
-  👨‍🎓 **Trường Đại Học**: Đại Học công Nghệ TP.HCM (HUTECH)
-  🆔 **MSSV**: 2180600307
-  📧 **Gmail**: dohuynh116@gmail.com
-  🐱 **Github**: [https://github.com/HTD-0307](https://github.com/HTD-0307)
-  🔗 **Link Workshop**:
## 1. 📄 Executive Summary

### Problem Statement
Quản lý kho thủ công gây sai sót kiểm kê (5-10% sản phẩm bị thiếu/dư), chậm trễ bổ sung hàng (24-48 giờ), và tăng chi phí vận hành. Theo báo cáo từ Wasp Barcode Technologies (2021), 43% doanh nghiệp nhỏ gặp vấn đề sai sót tồn kho, gây thiệt hại trung bình 5-10% doanh thu hàng năm.

### Solution Overview
Workshop này sẽ triển khai xây dựng hệ thống giám sát kho hàng thông minh, sử dụng cảm biến IoT để theo dõi số lượng hàng tồn kho trong thời gian thực, gửi cảnh báo khi hàng sắp hết, và cung cấp báo cáo tồn kho, tối ưu chi phí với AWS Free Tier.

### Business Benefits và ROI Summary
- **Lợi ích cho doanh nghiệp**: Tiết kiệm 20 giờ/tuần kiểm kê hàng thủ công, giảm 30% sai sót trong quá trình kiểm kê, tiết kiệm 15% chi phí bổ sung hàng nhờ cảnh báo kịp thời.
- **ROI**: Các dịch vụ AWS Free Tier sẽ giúp giảm thiểu chi phí cho giai đoạn phát triển và triển khai. Dự kiến ROI đạt 25% sau 6 tháng khi áp dụng tự động hóa quy trình.

### Investment Required và Timeline
- **Đầu tư cần thiết**: Chủ yếu sử dụng AWS Free Tier, chi phí phát triển ~100 giờ công (miễn phí nếu tự thực hiện).
- **Timeline**: Dự án dự kiến hoàn thành trong 3 tháng.

### Success Metrics và Expected Outcomes
- **Success Metrics**: Độ chính xác kiểm kê đạt 99%, giảm thời gian xử lý cảnh báo từ 224 giờ xuống 1 giờ.
- **Expected Outcomes**: Báo cáo tồn kho tự dộng, cải thiện hiệu quả vận hành.

## 2. 🎯 Problem Statement

### Current Situation Analysis
Hiện tại, nhiều kho hàng thương mại điện tử thường dùng bảng tính hoặc phần mềm không tích hợp IoT, dẩn đến sai sót trong quá trình kiểm kê, chậm trể việc bổ sung hàng hóa ảnh hưởng trực tiếp đến quyết định kinh doanh.

### Pain Points Identification
- Sai sót kiểm kê gây thiệt hại cho doanh thu và lòng tin từ khách hàng.
- Thời gian kiểm kê thủ công tốn thêm nhân sự thực hiện.
- Rủi ro hết hàng không bổ sung kịp thời.

### Stakeholders Affected và Their Concerns
- **Quản lý kho**: Cần dử liệu kho chính xác.
- **Nhà cung cấp**: Cần thông báo kịp thời để bổ sung hàng.
- **Khách hàng**: Mong sản phẩm luôn có sẳn.

### Business Consequences của Inaction
- Doanh nghiệp có thể thất thoát doanh thu, tăng chi phí nhân sự kiểm kê, giãm uy tính thương hiệu.

### Market Opportunity
- Hệ thống IoT giúp SMEs cạnh tranh được với các doanh nghiệp lớn hơn. Theo *MarketsandMarkets* (2022), thị trường IoT kho dự kiến đạt $19 tỷ vào 2026, tăng trưởng 15% mỗi năm.

## 3. 🏗️ Solution Architecture

### High-level Architecture Diagram
![Solution Architecture Diagram](/images/main_model_light.png)

### AWS Services Selection và Justification
- **AWS IoT Core**: Thu thập dữ liệu cảm biến. Miễn phí 2000 tin nhắn/tháng
- **AWS Lambda**: Dịch vụ serverless giúp xử lý dữ liệu, kiểm tra ngưỡng tồn kho và gửi cảnh báo. Miễn phí 1 triệu lượt gọi hàm mỗi tháng.
- **Amazon DynamoDB**: Lưu trữ tồn kho. Miễn phí 25GB bộ nhớ lưu trữ.
- **Amazon S3**: Lưu trữ ảnh và kết quả phân tích. Miễn phí 5GB bộ nhớ lưu trữ và 20,000 lượt truy xuất mỗi tháng.
- **Amazon SNS**: Gửi email cảnh báo. Miễn phí 1 triệu thông báo.
- **AWS CloudWatch**: Giám sát và ghi lại logs hệ thống để theo dõi hiệu suất và lỗi.
- **AWS IAM**: Quản lý quyền truy cập và bảo mật các dịch vụ AWS.

### Component Interactions và Data Flow
1. **IoT upload data**: Cảm biến gửi số lượng tồn kho qua AWS IoT Core.
2. **AWS IoT Core**: AWS IoT Core nhận dữ liệu từ cảm biến và sử dụng IoT Rule để chuyển tiếp dữ liệu này đến một Lambda function.
3. **AWS Lambda**: Lambda xử lý dử liệu,cập nhật dữ liệu vào DynamoDB, kiểm tra ngưỡng nếu thấp hơn sẽ kích hoạt SNS gửi email.
4. **S3**: Lưu dữ liệu các log.

### Security Architecture và Compliance
- **IAM Roles**: Đảm bảo rằng chỉ các dịch vụ và người dùng có quyền truy cập mới có thể thực hiện các hành động quan trọng trong hệ thống.
- **Data**: Dữ liệu sẽ được mã hóa trong DynamoDB và S3.

### Scalability và Performance Considerations
- **Lambda**: Tự động mở rộng theo tải, giúp xử lý hiệu quả khi có sự gia tăng lưu lượng và yêu cầu từ hệ thống.
- **DynamoDB**: Hỗ trợ mở rộng khả năng lưu trữ và tăng cường lưu lượng đọc/ghi, giúp duy trì hiệu suất tối ưu khi dữ liệu tăng trưởng.
- **IoT Core**: Có khả năng xử lý hàng triệu tin nhắn đồng thời, đảm bảo khả năng mở rộng mạnh mẽ khi số lượng thiết bị và dữ liệu IoT gia tăng

### Integration Points với Existing Systems
- Sử dụng API REST từ Lambda để đồng bộ dữ liệu và các thao tác giữa hệ thống hiện có như ERP/CRM và các dịch vụ khác thông qua API Gateway. Điều này giúp hệ thống kết nối mượt mà, bảo mật và dễ dàng mở rộng khi cần thiết.

## 4. 🔧 Technical Implementation

### Implementation Phases và Deliverables
1. **Giai đoạn 1**: Thiết kế hệ thống, giả lập cảm biến,thiết lập DynamoDB  (2 tuần)
2. **Giai đoạn 2**: Thiết lập IoT Core, triển khai Lambda functions, tích hợp SNS (3 tuần)
3. **Giai đoạn 3**: Lưu trữ log vào S3, kiểm tra tích hợp (2 tuần)
4. **Giai đoạn 4**: Triển khai, kiểm tra hiệu suất (1 tuần)

### Technical Requirements
- **Compute**: AWS Lambda (miễn phí 1 triệu lượt gọi mỗi tháng)
- **Storage**: DynamoDB (miễn phí 25GB bộ nhớ lưu trữ), S3 (miễn phí 5GB bộ nhớ lưu trữ)
- **Network**: IoT Core (MQTT, 2,000 tin nhắn Free Tier)

### Development Approach và Methodologies
- **Phương pháp phát triển**: Agile Development (2 tuần/sprint), Python sẽ được sử dụng để phát triển các hàm Lambda.

### Testing Strategy
- **Unit Testing**: kiểm tra từng hàm Lambda, đảm bảo các chức năng hoạt động chính xác và độc lập.
- **Integration Testing**: Kiểm tra tính đồng bộ và kết nối giữa IoT Core, Lambda và DynamoDB để đảm bảo các thành phần hệ thống hoạt động mượt mà và đồng nhấ.
- **Performance Testing**: Mô phỏng 1,000 tin nhắn IoT/ngày để đánh giá khả năng xử lý và đáp ứng của hệ thống trong môi trường thực tế.

### Deployment Plan và Rollback Procedures
- **Deployment Plan**: Triển khai qua AWS CLI, dùng CloudFormation để tự động hóa.
- **Rollback Procedures**: Sao lưu DynamoDB hàng ngày, lưu trữ log S3 với lifecycle policy.

### Configuration Management
- Sử dụng Git và AWS Systems Manager Parameter Store để quản lý cấu hình.

## 5. 📅 Timeline & Milestones

### Project Phases Breakdown
1. **Giai đoạn 1: Thiết kế và chuẩn bị** (1 tuần)
   - **Mục tiêu**: Thiết kế tổng quan hệ thống,giả lập cảm biến, cấu hình DynamoDB.
   - **Deliverables**: Phác thảo kiến trúc hệ thống, giả lập cảm biến, mô hình bảng DynamoDB.
   
2. **Giai đoạn 2: Phát triển và triển khai** (1 tuần)
   - **Mục tiêu**: Phát triển các hàm Lambda, tích hợp SNS, cấu hình IoT Core, tích hợp S3.
   - **Deliverables**: Mã nguồn Lambda, Email mẫu, quy tắt IoT Core, liên kêt S3.

3. **Giai đoạn 3: Kiểm thử và triển khai** (1 tuần)
   - **Mục tiêu**: Kiểm thử hệ thống và triển khai vào môi trường sản xuất.
   - **Deliverables**: Kiểm thử toàn bộ hệ thống, từ quy trình tải dữ liệu kho đến thông báo mail khi số lượng ượt ngưỡng, và triển khai hệ thống lên AWS.

### Key Milestones và Success Criteria
- **Milestone 1**: Hoàn thành thiết kế hệ thống và lựa chọn các dịch vụ AWS.
   - **Success Criteria**: Hoàn thành kiến trúc hệ thống với các dịch vụ AWS đã chọn, bao gồm IoT Core, Lambda, DynamoDB, S3 và SNS.
   - **Ngày hoàn thành dự kiến**: Ngày 7 sau khi bắt đầu dự án.

- **Milestone 2**: Hoàn thành phát triển Lambda và cấu hình IoT Core.
   - **Success Criteria**: Lambda function có thể kích hoạt thành công và IoT Core nhận dữ liệu từ cảm biến giả lập. Kết quả sẽ được trả về đúng định dạng JSON và lưu trữ trên DynamoDB.
   - **Ngày hoàn thành dự kiến**: Ngày 14 sau khi bắt đầu dự án.

- **Milestone 3**: Kiểm thử và triển khai hệ thống vào môi trường sản xuất.
   - **Success Criteria**: Hệ thống hoạt động ổn định trong môi trường sản xuất.
   - **Ngày hoàn thành dự kiến**: Ngày 21 sau khi bắt đầu dự án.

### Dependencies Identification
- **Phụ thuộc vào các dịch vụ AWS**: Đảm bảo các dịch vụ như Lambda, IoT Core, DynamoDB và S3 đã được cấu hình và hoạt động đúng. Cấu hình Lambda trước khi phát triển IoT Core và DynamoDB cần sẳn sàng trước khi tích hợp.
- **Phụ thuộc vào môi trường phát triển**: Các công cụ phát triển như Git, AWS CLI phải được cài đặt và cấu hình trước khi bắt đầu phát triển.

### Critical Path Analysis
- Các bước kiểm thử và tích hợp hệ thống có thể là điểm nghẽn, cần đảm bảo có đủ thời gian và tài nguyên cho các giai đoạn này. Nếu giai đoạn phát triển hoặc tích hợp gặp sự cố, sẽ ảnh hưởng đến tiến độ của các giai đoạn sau.

### Resource Allocation Plan
- **Nhân lực**: 1 sinh viên thực tập, 1 người hướng dẫn.
- **Công cụ**: AWS Console, Git, CloudFormation, Lambda, IoT Core.

### Buffer Time cho Risks
- Thêm 2 ngày cho các rủi ro phát sinh trong giai đoạn kiểm thử và triển khai.

## 6. 💰 Budget Estimation

### AWS Infrastructure Costs (Monthly/Annual)
- **Monthly**: Dự kiến miễn phí trong phạm vi AWS Free Tier, bao gồm:
  - **IoT Core**: Miễn phí 2,000 tin nhắn/tháng.
  - **AWS Lambda**: Miễn phí 1 triệu lượt gọi mỗi tháng.
  - **Amazon S3**: Miễn phí 5GB bộ nhớ lưu trữ và 20,000 lượt truy xuất mỗi tháng.
  - **DynamoDB**: 25GB bộ nhớ lưu trữ.
  - **AWS CloudWatch**: Miễn phí 5GB lưu trữ logs và 5GB dữ liệu gửi đi mỗi tháng.
  - **SNS**: Miễn phí 1 triệu thông báo email.

- **Annually**: Các chi phí hàng năm sẽ tương tự như các chi phí hàng tháng và sẽ phát sinh nếu vượt quá các giới hạn miễn phí. 

### Development Costs (One-time)
- **Chi phí nhân sự**: Dự án yêu cầu một sinh viên thực tập tham gia phát triển trong 3 tháng. Giả sử mỗi giờ công là $5, với tổng thời gian làm việc là 480 giờ (3 tháng x 160 giờ/tháng), chi phí nhân sự sẽ là:
  - **Chi phí nhân sự**: $5 * 480 = $2,400
- **Công cụ phát triển**: Không có chi phí phần mềm hoặc phần cứng phát sinh ngoài các dịch vụ AWS Free Tier. Các công cụ như Git, CloudFormation, AWS Console, và các IDE (VSCode, GitHub) đều miễn phí sử dụng.

### Third-party Services và Licenses
- **Third-party Services**: Trong phạm vi của dự án này, không yêu cầu bất kỳ dịch vụ bên ngoài nào ngoài AWS.
- **Licenses**: Không có phí cấp phép phát sinh, vì tất cả các dịch vụ AWS được sử dụng đều nằm trong phạm vi AWS Free Tier hoặc được tính phí theo mức độ sử dụng.

### Operational Costs (Ongoing)
- **Chi phí AWS hàng tháng**: 
  - **IoT Core**: Sau khi vượt quá 2,000 tin nhắn miễn phí, chi phí là $0.2 mỗi 100 tin nhắn IoT.
  - **AWS Lambda**: Sau khi vượt qua 1 triệu lượt gọi miễn phí, chi phí là $0.20 mỗi triệu lượt gọi.
  - **Amazon S3**: Sau khi vượt qua 5GB bộ nhớ lưu trữ miễn phí, chi phí là $0.023 mỗi GB/tháng.
  - **AWS CloudWatch**: Sau khi vượt qua 5GB logs miễn phí, chi phí là $0.03 mỗi GB.
  - **SNS**: Sau khi vượt 1 triệu thông báo mail miễn phí, chi phí là $2.00 cho 100.000 mail.

### ROI Calculation và Break-even Analysis
- **ROI (Return on Investment)**: Mặc dù dự án sử dụng AWS Free Tier trong giai đoạn thử nghiệm, chi phí có thể phát sinh khi vượt qua các giới hạn miễn phí. ROI dự kiến sẽ đạt 25% trong vòng 6 tháng, vì hệ thống sẽ tiết kiệm được chi phí nhân sự khi kiểm tra kho hàng.
  
- **Break-even Analysis**: 
  - Điểm hòa vốn dự kiến sẽ không xảy ra trong 6 tháng đầu do sử dụng AWS Free Tier. Sau khi vượt qua giới hạn miễn phí của AWS, chi phí sẽ bắt đầu phát sinh. 
  - Dự kiến break-even point có thể đạt được trong khoảng 12 tháng nếu hệ thống được mở rộng và sử dụng tối đa các tính năng tự động của AWS.

### Cost Optimization Strategies
- **Tận dụng AWS Free Tier**: Cố gắng giữ mức sử dụng các dịch vụ trong phạm vi miễn phí của AWS.
- **Auto-scaling**: Sử dụng tính năng tự động mở rộng của AWS Lambda và S3 để giảm thiểu chi phí khi không có tải cao.
- **Sử dụng CloudWatch**: Theo dõi chi tiết mức độ sử dụng các dịch vụ AWS để đảm bảo không vượt quá giới hạn miễn phí mà không cần thiết.
- **S3**: Xóa log sau 30 ngày để tiết kiệm chi phí.

## 7. ⚠️ Risk Assessment

### Risk Identification (Technical, Business, Operational)
1. **Technical Risks**:
   - **IoT Core cấu hình sai**: Cấu hình sai quy tắc MQTT, chứng chỉ thiết bị hoặc chính sách bảo mật trong AWS IoT Core có thể làm gián đoạn việc thu nhận dữ liệu từ cảm biến.
   - **Lỗi tích hợp hệ thống**: Lỗi trong tích hợp giữa AWS IoT Core, Lambda, DynamoDB, hoặc SNS có thể gây gián đoạn luồng dữ liệu hoặc chậm triển khai.

2. **Business Risks**:
   - **Dữ liệu cảm biến không chính xác**: Cảm biến IoT (giả lập hoặc thực tế) cung cấp dữ liệu sai lệch, dẫn đến cảnh báo không đúng hoặc quyết định kinh doanh sai lầm (e.g., bổ sung hàng không cần thiết).
   - **Không đạt được lợi ích kinh doanh mong đợi**: Hệ thống không đạt mục tiêu giảm 30% sai sót kiểm kê hoặc 15% chi phí bổ sung hàng, làm giảm ROI.
3. **Operational Risks**:
   - **Vượt giới hạn AWS Free Tier**: Lưu lượng tin nhắn IoT, lưu trữ DynamoDB/S3 hoặc yêu cầu Lambda vượt quá giới hạn Free Tier, gây phát sinh chi phí ngoài dự kiến.
   - **Mất dữ liệu hoặc lỗi khôi phục**: Lỗi trong sao lưu DynamoDB hoặc chính sách vòng đời S3 dẫn đến mất dữ liệu tồn kho hoặc log, gây sai lệch kiểm kê.
### Impact Assessment và Probability Analysis
- **Technical Risks**:
  - **IoT Core cấu hình sai**:
    - **Impact**: Trung bình, làm chậm xử lý dữ liệu 1-2 ngày, gây sai lệch tạm thời trong dữ liệu tồn kho.
    - **Probability**: Thấp, vì sử dụng AWS Device Simulator để kiểm tra cấu hình trước triển khai.
  
  - **Lỗi tích hợp hệ thống**:
    - **Impact**: Trung bình, chậm triển khai 1-2 tuần, ảnh hưởng đến lịch trình.
    - **Probability**: Thấp, sử dụng AWS CloudFormation để tự động hóa triển khai.

- **Business Risks**:
  - **Dữ liệu cảm biến không chính xác**:
    - **Impact**: Cao, vì có thể sai lệch tồn kho gây hủy đơn hoặc dư thừa, thiệt hại doanh thu và giãm uy tín thương hiệu.
    - **Probability**: Thấp, vì áp dụng quy tắc Lambda để phát hiện dữ liệu bất thường (e.g., giá trị ngoài phạm vi).

  - **Không đạt được lợi ích kinh doanh mong đợi**:
    - **Impact**: Cao, ảnh hưởng đến thời gian hoàn vốn, ROI giãm.
    - **Probability**: Thấp, vì AWS đã cung cấp các công cụ bảo mật mạnh mẽ.

- **Operational Risks**:
  - **Vượt giới hạn AWS Free Tier**:
    - **Impact**: Thấp, chi phí thêm ~$0.2/tháng cho 100 tin nhắn IoT hoặc $0.1/GB S3.
    - **Probability**: Thấp, vì theo dõi chi phí hàng tuần qua AWS Budgets, đặt cảnh báo khi đạt 80% giới hạn Free Tier.

  - **Mất dữ liệu hoặc lỗi khôi phục**:
    - **Impact**: Cao, gây tê liệt quá trình kinh doanh.
    - **Probability**: Thấp, vì áp dụng chính sách vòng đời S3 để lưu trữ log tối thiểu 30 ngày.

### Risk Matrix với Prioritization
| Risk Type               | Impact | Probability | Mitigation Strategy                          |
|-------------------------|--------|-------------|----------------------------------------------|
| **Technical Risk**       |        |             |                                              |
| IoT Core cấu hình sai | Medium   | Low         | Tài liệu AWS, Device Simulator, xác nhận cấu hình |
| Lỗi tích hợp hệ thống | Medium | Low      | Kiểm tra tích hợp, CloudFormation, dự phòng 1 tuần |
| **Business Risk**        |        |             |                                              |
| Dữ liệu cảm biến không chính xác | High   | Low      | Kiểm tra cảm biến, phát hiện bất thường, so sánh thủ công |
| Không đạt được lợi ích kinh doanh mong đợi | High   | Low         | Thu thập dữ liệu cơ sở, kiểm toán hàng quý, tinh chỉnh ngưỡng |
| **Operational Risk**     |        |             |                                              |
| Vượt giới hạn AWS Free Tier | High   | Low      | AWS Budgets, tối ưu truy vấn, xóa log S3 |
| Mất dữ liệu hoặc lỗi khôi phục | High   | Low         | Sao lưu DynamoDB, chính sách S3, kiểm tra khôi phục |

### Mitigation Strategies cho Each Risk
- **Hệ thống không hoạt động khi tích hợp Rekognition**:
  - Kiểm tra và thử nghiệm tích hợp Rekognition trong môi trường phát triển trước khi triển khai vào sản xuất.
  - Sử dụng các API chính thức và tài liệu của AWS để đảm bảo tính tương thích.

- **Hiệu suất Lambda không đáp ứng yêu cầu**:
  - Cấu hình tối ưu cho các hàm Lambda để tránh các vấn đề về hiệu suất khi có quá nhiều yêu cầu đồng thời.
  - Sử dụng AWS CloudWatch để theo dõi và điều chỉnh cấu hình Lambda theo nhu cầu thực tế.

- **Khách hàng không chấp nhận công nghệ mới**:
  - Tổ chức các buổi đào tạo cho khách hàng để họ hiểu rõ lợi ích của công nghệ AI.
  - Cung cấp tài liệu chi tiết và hỗ trợ kỹ thuật khi khách hàng triển khai.

- **Không đáp ứng yêu cầu bảo mật và quyền riêng tư**:
  - Đảm bảo hệ thống tuân thủ các quy chuẩn bảo mật quốc tế như GDPR, HIPAA.
  - Cấu hình AWS IAM đúng cách để kiểm soát quyền truy cập vào dữ liệu.

- **Quá tải khi có quá nhiều yêu cầu đồng thời**:
  - Sử dụng tính năng Auto-scaling của AWS Lambda để hệ thống tự động mở rộng khi cần thiết.
  - Sử dụng AWS API Gateway để phân phối tải cho các API.

- **Sự cố trong việc xử lý dữ liệu và bảo mật**:
  - Sử dụng dịch vụ sao lưu dữ liệu tự động của AWS và thực hiện các biện pháp bảo mật như mã hóa dữ liệu.

### Contingency Plans
- **Technical Risks**: Nếu hệ thống gặp sự cố tích hợp, chúng ta sẽ có kế hoạch quay lại phiên bản trước đó và làm việc với đội ngũ AWS support để khắc phục.
- **Business Risks**: Nếu khách hàng không chấp nhận công nghệ, sẽ cung cấp thêm tài liệu và hỗ trợ để khách hàng hiểu rõ giá trị của AI. Nếu không thể triển khai, sẽ xem xét điều chỉnh công nghệ phù hợp với yêu cầu của khách hàng.
- **Operational Risks**: Trong trường hợp hệ thống quá tải, sẽ tạm thời tăng cường tài nguyên (ví dụ, tăng số lượng phiên bản Lambda) hoặc áp dụng biện pháp giảm tải.

### Monitoring và Escalation Procedures
- **Monitoring**: Sử dụng AWS CloudWatch để giám sát hiệu suất và lỗi hệ thống. Đặt ngưỡng cảnh báo khi có lỗi hệ thống.
- **Escalation Procedures**: Nếu có sự cố lớn xảy ra, sẽ thông báo ngay cho người quản lý dự án và nhóm hỗ trợ kỹ thuật AWS để xử lý nhanh chóng.

## 8. 🎯 Expected Outcomes

### Success Metrics
- **Technical**: Thời gian phản hồi dưới 5 giây, độ chính xác nhận diện đạt 95%.
- **Business**: Tiết kiệm chi phí phân tích ảnh và tăng hiệu quả công việc.

### Short-term Benefits (0-6 months)
- Tiết kiệm chi phí phân tích ảnh.

### Medium-term Benefits (6-18 months)
- Tăng trưởng doanh thu nhờ tự động hóa quy trình phân tích ảnh.

### Long-term Value (18+ months)
- Mở rộng ứng dụng AI trong các lĩnh vực khác để tạo lợi thế cạnh tranh.

### User Experience Improvements
- Trải nghiệm người dùng sẽ được cải thiện với hệ thống tự động nhận diện ảnh chính xác và nhanh chóng.

### Strategic Capabilities Gained
- Cải thiện hiệu quả công việc và tạo lợi thế cạnh tranh thông qua tự động hóa.
