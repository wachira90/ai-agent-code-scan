# AI AGENTS สำหรับสั่ง AI ตรวจสอบ Source Code

AGENTS.md สำหรับสั่ง AI ตรวจสอบ Source Code แนวทางคล้าย SonarQube และ SAST เรียบร้อยแล้ว โดยเน้นรายงานเชิงลึกและคำแนะนำแก้ไขที่ใช้งานได้จริง

เนื้อหาหลักภายในไฟล์ครอบคลุม:

- ตรวจช่องโหว่ตาม OWASP Top 10, OWASP API Security Top 10, CWE และ OWASP ASVS
- ตรวจ SQL Injection, Command Injection, XSS, SSRF, IDOR/BOLA, Authentication และ Authorization
- ตรวจ Secrets, Cryptography, File Upload, Path Traversal และ Unsafe Deserialization
- ตรวจ Dependency, Supply Chain, SBOM และ package ที่มีความเสี่ยง
- ตรวจ Dockerfile, Kubernetes, Terraform, Cloud IAM และ CI/CD pipeline
- ตรวจ Bug, Code Smell, Complexity, Duplication, Reliability และ Performance
- แยก Confirmed, Likely, Needs Verification และ Informational เพื่อลด False Positive
- กำหนด Severity, Confidence, CVSS และลำดับความสำคัญ P0-P4
- มี Quality Gate แบบ PASS, WARN และ FAIL
- กำหนดรูปแบบรายงานพร้อม file, line, symbol, data flow, source และ sink
- ให้ตัวอย่างโค้ดก่อนและหลังแก้ไข
- แนะนำ Regression Test และ Security Test สำหรับแต่ละช่องโหว่
- มี Remediation Roadmap ตั้งแต่ 24 ชั่วโมงถึง 90 วัน
- รองรับผลลัพธ์แบบ Markdown และ security-findings.json
- กำหนดไม่ให้ AI แก้ Source Code จนกว่าจะได้รับคำสั่งโดยตรง
- มี Prompt ตัวอย่างสำหรับเริ่มสแกน Repository อยู่ท้ายไฟล์

## ตัวอย่างคำสั่งใช้งาน

```
Scan repository นี้แบบ security และ code quality review ตาม AGENTS.md
ให้ตรวจทั้ง first-party code, dependencies, secrets, Docker/Kubernetes/IaC และ CI/CD
สร้างรายงาน Markdown แบบละเอียด เรียงตาม severity พร้อม file/line, CWE, OWASP,
confidence, data flow, impact, remediation, before/after code, tests, quality gate
และ remediation roadmap โดยห้ามแก้ source code จนกว่าจะได้รับคำสั่ง
```

## แนวทางที่ปรับปรุง

ไฟล์นี้ไม่ได้ให้ AI ค้นหาจาก keyword เท่านั้น แต่กำหนดให้ติดตาม Source → Validation → Authorization Boundary → Sink พร้อมตรวจสอบ compensating controls และยืนยัน Critical/High ด้วยหลักฐานก่อนรายงาน ช่วยให้ผลลัพธ์มีรายละเอียดและลด False Positive มากกว่าการใช้ prompt สั้นทั่วไป

