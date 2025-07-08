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
Quản lý kho hàng thủ công dẫn đến sai sót trong kiểm kê, chậm trễ trong bổ sung hàng, và tăng chi phí vận hành (ước tính lãng phí 5-10% doanh thu do tồn kho không tối ưu).

### Solution Overview
Workshop này sẽ triển khai xây dựng hệ thống giám sát kho hàng thông minh, sử dụng cảm biến IoT để theo dõi số lượng hàng tồn kho trong thời gian thực, gửi cảnh báo khi hàng sắp hết, và cung cấp báo cáo tồn kho, tối ưu chi phí với AWS Free Tier.

### Business Benefits và ROI Summary
- **Lợi ích cho doanh nghiệp**: Giảm 30% sai sót trong quá trình kiểm kê, tiết kiệm 15% chi phí bổ sung hàng nhờ cảnh báo kịp thời.
- **ROI**: Các dịch vụ AWS Free Tier sẽ giúp giảm thiểu chi phí cho giai đoạn phát triển và triển khai. Dự kiến ROI đạt 25% sau 6 tháng khi áp dụng tự động hóa quy trình.

### Investment Required và Timeline
- **Đầu tư cần thiết**: Chủ yếu sử dụng AWS Free Tier, chi phí phát triển ~100 giờ công (miễn phí nếu tự thực hiện).
- **Timeline**: Dự án dự kiến hoàn thành trong 3 tháng.

### Success Metrics và Expected Outcomes
- **Success Metrics**: Thời gian phản hồi hệ thống dưới 5 giây, độ chính xác nhận diện ảnh đạt 95%.
- **Expected Outcomes**: Cải thiện hiệu quả công việc và giảm thiểu sai sót trong phân tích ảnh.

## 2. 🎯 Problem Statement

### Current Situation Analysis
Hiện tại, nhiều doanh nghiệp sử dụng các phương pháp thủ công hoặc các công cụ không hiệu quả để phân tích hình ảnh, gây lãng phí thời gian và chi phí.

### Pain Points Identification
- Thời gian xử lý ảnh lâu, ảnh hưởng đến hiệu quả công việc.
- Độ chính xác trong nhận diện ảnh chưa cao khi sử dụng các công cụ thủ công.

### Stakeholders Affected và Their Concerns
- **Doanh nghiệp**: Lo ngại về chi phí và hiệu quả của hệ thống.
- **Nhân viên**: Lo ngại về việc sử dụng công cụ mới và khả năng tự động hóa.

### Business Consequences của Inaction
- Doanh nghiệp có thể mất cơ hội cạnh tranh và lãng phí nguồn lực nếu không cải thiện quy trình nhận diện ảnh.

### Market Opportunity
- Thị trường AI nhận diện ảnh đang phát triển mạnh mẽ, đặc biệt trong các lĩnh vực như bán lẻ, y tế và an ninh.

## 3. 🏗️ Solution Architecture

### High-level Architecture Diagram
![Solution Architecture Diagram](/images/main_model_light.png)

### AWS Services Selection và Justification
- **Amazon Rekognition**: Dịch vụ nhận diện ảnh mạnh mẽ từ AWS, miễn phí trong giới hạn 5,000 ảnh mỗi tháng.
- **AWS Lambda**: Dịch vụ serverless giúp giảm chi phí và tối ưu hóa hiệu quả. Miễn phí 1 triệu lượt gọi hàm mỗi tháng.
- **Amazon S3**: Lưu trữ ảnh và kết quả phân tích. Miễn phí 5GB bộ nhớ lưu trữ và 20,000 lượt truy xuất mỗi tháng.
- **AWS API Gateway**: Quản lý các API để kết nối frontend với hệ thống backend.
- **AWS CloudWatch**: Giám sát và ghi lại logs hệ thống để theo dõi hiệu suất và lỗi.
- **AWS IAM**: Quản lý quyền truy cập và bảo mật các dịch vụ AWS.

### Component Interactions và Data Flow
1. **User Uploads Image**: Người dùng tải ảnh lên qua giao diện frontend.
2. **API Gateway**: API Gateway nhận yêu cầu HTTP POST từ frontend và kích hoạt Lambda function.
3. **AWS Lambda**: Lambda xử lý ảnh, gửi đến Amazon Rekognition để phân tích.
4. **Amazon Rekognition**: Phân tích ảnh và trả về kết quả JSON.
5. **S3 Storage**: Lưu ảnh và kết quả phân tích vào Amazon S3.
6. **CloudWatch**: Ghi logs về quá trình xử lý và phân tích ảnh.
7. **Return Results**: Kết quả phân tích ảnh và hình ảnh sẽ được trả về cho người dùng qua frontend.

### Security Architecture và Compliance
- **IAM Roles**: Đảm bảo rằng chỉ các dịch vụ và người dùng có quyền truy cập mới có thể thực hiện các hành động quan trọng trong hệ thống.
- **Data Encryption**: Dữ liệu sẽ được mã hóa khi lưu trữ trong S3 và khi truyền tải qua mạng.

### Scalability và Performance Considerations
- Hệ thống serverless tự động mở rộng khi có nhiều yêu cầu, giúp duy trì hiệu suất cao và tiết kiệm chi phí.
- Sử dụng Lambda giúp tự động mở rộng tài nguyên khi cần thiết mà không phải lo lắng về quản lý máy chủ.

### Integration Points với Existing Systems
- Hệ thống có thể dễ dàng tích hợp với các hệ thống quản lý khách hàng hiện có hoặc các ứng dụng dữ liệu khác.

## 4. 🔧 Technical Implementation

### Implementation Phases và Deliverables
1. **Giai đoạn 1**: Thiết kế hệ thống và lựa chọn dịch vụ AWS (2 tuần)
2. **Giai đoạn 2**: Phát triển và triển khai Lambda functions, cấu hình Rekognition (4 tuần)
3. **Giai đoạn 3**: Kiểm thử và triển khai toàn hệ thống (4 tuần)

### Technical Requirements
- **Compute**: AWS Lambda (miễn phí 1 triệu lượt gọi mỗi tháng)
- **Storage**: Amazon S3 (miễn phí 5GB bộ nhớ lưu trữ)
- **Network**: AWS API Gateway (miễn phí 1 triệu yêu cầu mỗi tháng)

### Development Approach và Methodologies
- **Phương pháp phát triển**: Agile Development, áp dụng CI/CD cho quy trình triển khai.

### Testing Strategy
- **Unit Testing**: Kiểm thử các hàm Lambda riêng biệt.
- **Integration Testing**: Kiểm thử kết nối giữa các dịch vụ AWS.
- **Performance Testing**: Kiểm tra hiệu suất hệ thống khi xử lý nhiều yêu cầu đồng thời.

### Deployment Plan và Rollback Procedures
- **Deployment Plan**: Triển khai qua AWS CloudFormation và API Gateway.
- **Rollback Procedures**: Quay lại phiên bản trước nếu gặp lỗi nghiêm trọng trong quá trình triển khai.

### Configuration Management
- Sử dụng Git và AWS CloudFormation để quản lý cấu hình.

## 5. 📅 Timeline & Milestones

### Project Phases Breakdown
1. **Giai đoạn 1: Thiết kế và lập kế hoạch** (1 tuần)
   - **Mục tiêu**: Thiết kế tổng quan hệ thống và lựa chọn các dịch vụ AWS.
   - **Deliverables**: Phác thảo kiến trúc hệ thống, danh sách các dịch vụ AWS cần sử dụng.
   
2. **Giai đoạn 2: Phát triển và triển khai** (1 tuần)
   - **Mục tiêu**: Phát triển các hàm Lambda, cấu hình Amazon Rekognition và kết nối với S3.
   - **Deliverables**: Mã nguồn Lambda, cấu hình Rekognition, S3 bucket để lưu trữ ảnh và kết quả phân tích.

3. **Giai đoạn 3: Kiểm thử và triển khai** (1 tuần)
   - **Mục tiêu**: Kiểm thử hệ thống và triển khai vào môi trường sản xuất.
   - **Deliverables**: Kiểm thử toàn bộ hệ thống, từ việc tải ảnh lên cho đến trả kết quả phân tích, và triển khai hệ thống lên AWS.

### Key Milestones và Success Criteria
- **Milestone 1**: Hoàn thành thiết kế hệ thống và lựa chọn các dịch vụ AWS.
   - **Success Criteria**: Hoàn thành kiến trúc hệ thống với các dịch vụ AWS đã chọn, bao gồm IAM, Lambda, Rekognition, S3, và API Gateway.
   - **Ngày hoàn thành dự kiến**: Ngày 7 sau khi bắt đầu dự án.

- **Milestone 2**: Hoàn thành phát triển Lambda và tích hợp Rekognition.
   - **Success Criteria**: Lambda function có thể kích hoạt thành công và sử dụng Rekognition để phân tích ảnh. Kết quả sẽ được trả về đúng định dạng JSON và lưu trữ trên S3.
   - **Ngày hoàn thành dự kiến**: Ngày 14 sau khi bắt đầu dự án.

- **Milestone 3**: Kiểm thử và triển khai hệ thống vào môi trường sản xuất.
   - **Success Criteria**: Hệ thống hoạt động ổn định trong môi trường sản xuất, với thời gian phản hồi dưới 5 giây và độ chính xác nhận diện ảnh đạt 95%.
   - **Ngày hoàn thành dự kiến**: Ngày 21 sau khi bắt đầu dự án.

### Dependencies Identification
- **Phụ thuộc vào các dịch vụ AWS**: Đảm bảo các dịch vụ như Lambda, Rekognition, API Gateway và S3 đã được cấu hình và hoạt động đúng.
- **Phụ thuộc vào môi trường phát triển**: Các công cụ phát triển như Git, AWS SDK phải được cài đặt và cấu hình trước khi bắt đầu phát triển.

### Critical Path Analysis
- Các bước kiểm thử và tích hợp hệ thống có thể là điểm nghẽn, cần đảm bảo có đủ thời gian và tài nguyên cho các giai đoạn này. Nếu giai đoạn phát triển hoặc tích hợp gặp sự cố, sẽ ảnh hưởng đến tiến độ của các giai đoạn sau.

### Resource Allocation Plan
- **Nhân lực**: 1 sinh viên thực tập, 1 người hướng dẫn.
- **Công cụ**: AWS Console, Git, CloudFormation, Lambda, API Gateway.

### Buffer Time cho Risks
- Thêm 2 ngày cho các rủi ro phát sinh trong giai đoạn kiểm thử và triển khai.

## 6. 💰 Budget Estimation

### AWS Infrastructure Costs (Monthly/Annual)
- **Monthly**: Dự kiến miễn phí trong phạm vi AWS Free Tier, bao gồm:
  - **Amazon Rekognition**: Miễn phí 5,000 ảnh phân tích mỗi tháng.
  - **AWS Lambda**: Miễn phí 1 triệu lượt gọi mỗi tháng.
  - **Amazon S3**: Miễn phí 5GB bộ nhớ lưu trữ và 20,000 lượt truy xuất mỗi tháng.
  - **AWS API Gateway**: Miễn phí 1 triệu yêu cầu mỗi tháng.
  - **AWS CloudWatch**: Miễn phí 5GB lưu trữ logs và 5GB dữ liệu gửi đi mỗi tháng.

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
  - **Amazon Rekognition**: Sau khi vượt quá 5,000 ảnh miễn phí, chi phí là $1.00 mỗi 1,000 ảnh.
  - **AWS Lambda**: Sau khi vượt qua 1 triệu lượt gọi miễn phí, chi phí là $0.20 mỗi triệu lượt gọi.
  - **Amazon S3**: Sau khi vượt qua 5GB bộ nhớ lưu trữ miễn phí, chi phí là $0.023 mỗi GB/tháng.
  - **AWS API Gateway**: Sau khi vượt qua 1 triệu yêu cầu miễn phí, chi phí là $3.50 mỗi triệu yêu cầu.
  - **AWS CloudWatch**: Sau khi vượt qua 5GB logs miễn phí, chi phí là $0.03 mỗi GB.

### ROI Calculation và Break-even Analysis
- **ROI (Return on Investment)**: Mặc dù dự án sử dụng AWS Free Tier trong giai đoạn thử nghiệm, chi phí có thể phát sinh khi vượt qua các giới hạn miễn phí. ROI dự kiến sẽ đạt 25% trong vòng 6 tháng, vì hệ thống sẽ tiết kiệm được chi phí nhân sự và thời gian khi tự động hóa quy trình nhận diện ảnh.
  
- **Break-even Analysis**: 
  - Điểm hòa vốn dự kiến sẽ không xảy ra trong 6 tháng đầu do sử dụng AWS Free Tier. Sau khi vượt qua giới hạn miễn phí của AWS, chi phí sẽ bắt đầu phát sinh. 
  - Dự kiến break-even point có thể đạt được trong khoảng 12 tháng nếu hệ thống được mở rộng và sử dụng tối đa các tính năng tự động của AWS.

### Cost Optimization Strategies
- **Tận dụng AWS Free Tier**: Cố gắng giữ mức sử dụng các dịch vụ trong phạm vi miễn phí của AWS.
- **Auto-scaling**: Sử dụng tính năng tự động mở rộng của AWS Lambda và S3 để giảm thiểu chi phí khi không có tải cao.
- **Sử dụng CloudWatch**: Theo dõi chi tiết mức độ sử dụng các dịch vụ AWS để đảm bảo không vượt quá giới hạn miễn phí mà không cần thiết.
- **Reserved Instances (RI)**: Xem xét sử dụng **Reserved Instances** nếu hệ thống có nhu cầu sử dụng lâu dài, để nhận chiết khấu và giảm chi phí.
- **Sử dụng Layered Architecture**: Tối ưu kiến trúc bằng cách chỉ kích hoạt các tài nguyên cần thiết trong các tình huống cụ thể, giảm bớt việc sử dụng các tài nguyên tính phí liên tục.

## 7. ⚠️ Risk Assessment

### Risk Identification (Technical, Business, Operational)
1. **Technical Risks**:
   - **Hệ thống không hoạt động như mong đợi khi tích hợp Rekognition**: Có thể gặp phải các vấn đề khi kết nối các dịch vụ AWS, đặc biệt khi sử dụng Rekognition để phân tích ảnh.
   - **Hiệu suất Lambda không đáp ứng yêu cầu**: Lambda có thể gặp vấn đề khi có quá nhiều yêu cầu đồng thời, ảnh hưởng đến thời gian phản hồi.

2. **Business Risks**:
   - **Khách hàng không chấp nhận công nghệ mới**: Doanh nghiệp có thể không sẵn sàng thay đổi quy trình hiện tại và áp dụng công nghệ AI mới.
   - **Không đáp ứng được yêu cầu về tính bảo mật và quyền riêng tư**: Nếu hệ thống không tuân thủ các tiêu chuẩn bảo mật và quyền riêng tư, có thể gây mất lòng tin và ảnh hưởng đến doanh thu.

3. **Operational Risks**:
   - **Quá tải khi có quá nhiều yêu cầu đồng thời**: Khi có nhiều người dùng sử dụng hệ thống cùng lúc, có thể dẫn đến quá tải, làm giảm hiệu suất hệ thống.
   - **Sự cố trong việc xử lý dữ liệu và bảo mật**: Nếu không được quản lý đúng cách, dữ liệu có thể bị rò rỉ hoặc bị thao túng, ảnh hưởng đến uy tín và hoạt động của hệ thống.

### Impact Assessment và Probability Analysis
- **Technical Risks**:
  - **Hệ thống không hoạt động như mong đợi khi tích hợp Rekognition**:
    - **Impact**: Cao, vì sẽ ảnh hưởng trực tiếp đến tính năng chính của hệ thống (nhận diện ảnh).
    - **Probability**: Thấp, vì Rekognition được hỗ trợ tốt và đã được kiểm chứng.
  
  - **Hiệu suất Lambda không đáp ứng yêu cầu**:
    - **Impact**: Trung bình, nếu không xử lý kịp thời sẽ làm giảm hiệu suất hệ thống.
    - **Probability**: Trung bình, đặc biệt nếu có sự gia tăng lượng người dùng.

- **Business Risks**:
  - **Khách hàng không chấp nhận công nghệ mới**:
    - **Impact**: Cao, vì có thể ảnh hưởng đến khả năng triển khai hệ thống và mở rộng thị trường.
    - **Probability**: Trung bình, vì có thể cần một thời gian để khách hàng làm quen với công nghệ mới.

  - **Không đáp ứng yêu cầu về bảo mật và quyền riêng tư**:
    - **Impact**: Cao, ảnh hưởng lớn đến sự tin tưởng của khách hàng.
    - **Probability**: Thấp, vì AWS đã cung cấp các công cụ bảo mật mạnh mẽ.

- **Operational Risks**:
  - **Quá tải khi có quá nhiều yêu cầu đồng thời**:
    - **Impact**: Cao, ảnh hưởng đến trải nghiệm người dùng.
    - **Probability**: Trung bình, đặc biệt nếu không có biện pháp mở rộng phù hợp.

  - **Sự cố trong việc xử lý dữ liệu và bảo mật**:
    - **Impact**: Rất cao, có thể dẫn đến việc mất dữ liệu hoặc vi phạm bảo mật.
    - **Probability**: Thấp, nếu hệ thống được cấu hình đúng cách.

### Risk Matrix với Prioritization
| Risk Type               | Impact | Probability | Mitigation Strategy                          |
|-------------------------|--------|-------------|----------------------------------------------|
| **Technical Risk**       |        |             |                                              |
| Hệ thống không hoạt động khi tích hợp Rekognition | High   | Low         | Kiểm thử trước khi triển khai, sử dụng Rekognition SDK chính thức |
| Hiệu suất Lambda không đáp ứng yêu cầu | Medium | Medium      | Sử dụng AWS Lambda với cấu hình tối ưu, theo dõi hiệu suất qua CloudWatch |
| **Business Risk**        |        |             |                                              |
| Khách hàng không chấp nhận công nghệ mới | High   | Medium      | Cung cấp đào tạo và tài liệu giải thích về lợi ích của AI |
| Không đáp ứng yêu cầu bảo mật và quyền riêng tư | High   | Low         | Sử dụng các công cụ bảo mật AWS như IAM, VPC, và mã hóa dữ liệu |
| **Operational Risk**     |        |             |                                              |
| Quá tải khi có quá nhiều yêu cầu | High   | Medium      | Sử dụng Auto-scaling và thiết lập cân bằng tải với AWS Lambda |
| Sự cố trong việc xử lý dữ liệu và bảo mật | High   | Low         | Đảm bảo tuân thủ các quy trình bảo mật và thực hiện sao lưu thường xuyên |

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
