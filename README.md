<h1>☁️ CloudApp Project – AWS Full Stack Deployment</h1>

<h2>📌 Overview</h2>
<p>This project demonstrates a scalable and secure cloud architecture using AWS and CI/CD.</p>

<ul>
  <li><b>Frontend:</b> React (S3 + CloudFront)</li>
  <li><b>Backend:</b> Docker (EC2 + Auto Scaling)</li>
  <li><b>Database:</b> PostgreSQL (RDS)</li>
  <li><b>CI/CD:</b> GitHub Actions</li>
</ul>

<hr>

<h2>🌐 Networking</h2>

<h3>Subnets</h3>
<ul>
  <li>Public Subnets → ALB, NAT Gateway</li>
  <li>Private Subnets → EC2, RDS</li>
</ul>

<h3>Route Tables</h3>
<p><b>Public:</b> 0.0.0.0/0 → Internet Gateway</p>
<p><b>Private:</b> 0.0.0.0/0 → NAT Gateway</p>

<hr>

<h2>🔐 Security Groups</h2>

<ul>
  <li><b>ALB:</b> HTTP (80), HTTPS (443)</li>
  <li><b>EC2:</b> Port 5000 only from ALB</li>
  <li><b>RDS:</b> Port 5432 only from EC2</li>
</ul>

<p><b>Security Strategy:</b></p>
<ul>
  <li>Backend is not publicly accessible</li>
  <li>Database is private</li>
  <li>Access restricted between layers</li>
</ul>

<hr>

<h2>⚙️ Compute Layer</h2>
<ul>
  <li>EC2 with Auto Scaling for scalability</li>
  <li>Launch Template for configuration</li>
  <li>User Data script for Docker setup</li>
</ul>

<hr>

<h2>⚖️ Load Balancer</h2>
<ul>
  <li>Application Load Balancer distributes traffic</li>
  <li>Target Group performs health checks</li>
</ul>

<hr>

<h2>🗄 Database</h2>
<p>Amazon RDS (PostgreSQL) – Managed, secure, scalable</p>

<hr>

<h2>🎨 Frontend</h2>
<ul>
  <li>S3 for static hosting</li>
  <li>CloudFront for CDN</li>
</ul>

<hr>

<h2>🐳 CI/CD Pipeline</h2>
<ol>
  <li>Push code to GitHub</li>
  <li>Build Docker image</li>
  <li>Push to Docker Hub</li>
  <li>Update Launch Template</li>
  <li>Refresh Auto Scaling Group</li>
  <li>Deploy frontend to S3</li>
  <li>Invalidate CloudFront cache</li>
</ol>

<hr>

<h2>🎤 Interview Summary</h2>
<p>
This project uses a cloud-native architecture where the frontend is delivered via CloudFront,
the backend runs on Docker containers in EC2 with Auto Scaling, and the database is managed in RDS.
CI/CD is automated using GitHub Actions.
</p>
