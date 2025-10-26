1. Caching: From AWS ElasticCache to Open-Source Redis
What we used Before

We relied on AWS ElastiCache (Redis) for caching data like page content, user sessions, etc. It worked well but came with a high cost, especially as the number of nodes increased.

aws
What we use Now

We moved to:

Redis (open-source) hosted on our own EC2 instances
Grafana for monitoring cache hit/miss ratio and performance
We now only pay for EC2 compute cost (not for managed Redis service).

Savings

Cost dropped by 60–70%
More control over performance tuning
Visual insights using Grafana
2. Optimizing Video Delivery
The National Skill Up Portal by GeeksforGeeks is an e-learning platform offering free video-based skill development across India. With lakhs of learners daily, delivering smooth, fast, and cost-effective video access became essential.

Initial Challenges:

1. Videos were served directly from the origin (Amazon S3/EC2).

2. Every request, even from nearby users, fetched data from the origin.

3. Issues faced:

High AWS bandwidth costs
Slow performance in remote regions due to latency
before_using_origin_server
Solution: Integrating Amazon CloudFront for Edge Caching

To resolve this, the development team integrated Amazon CloudFront, a Content Delivery Network (CDN) that delivers content from edge locations closer to users.

Key Benefits:
Edge Caching for 1 Year:
Videos are cached at edge locations after first access. Future requests are served locally, reducing load on the origin.
50–70% Bandwidth Cost Reduction:
Most traffic now goes through CloudFront, cutting AWS transfer costs significantly.
Faster Access Nationwide:
Students across all regions now experience smoother playback with minimal buffering.
after_using_amazon_cloudfront_cdn
3. Smart Automation: Stop EC2 Instances After Work Hours
What was Happening

Our development/testing EC2 instances were running 24x7 — even when no one was using them at night.

2
What we Did

We wrote a Bash script + Cronjob combo:

Automatically stops EC2 instances at 10 PM
Starts them again at 9 AM
Fully automated with no human effort
Savings

No charges for idle machines at night
Saved 50% compute cost on dev/test infra
Easy to maintain
If you are new to cloud computing and unfamiliar with the AWS services or DevOps tools mentioned above, don't worry we’ll explain each of them in detail as we move forward in this course.

DevOps Model
Here is how the DevOps model flow works:

devopsmodel
Stages of DevOps are:

Build Stage
1. Developers write and organize code, using version control tools like Git to track changes.

2. The system automatically compiles and packages the code into a deployable format.

3. Dependencies (external libraries and tools) are included to ensure smooth operation.

4. Common Tools: Git, Jenkins, GitLab CI/CD, Gradle, Maven.

Test Stage
1. The software undergoes thorough testing to catch bugs and security risks before release.

2. Different testing methods include:

Unit Testing: Checks individual pieces of code.
Integration Testing: Ensures different parts of the system work together.
Performance Testing: Measures speed and scalability.
Security Testing: Identifies potential vulnerabilities.
3. Automated tests help ensure the software is stable before moving forward.

4. Common Tools: Selenium, JUnit, TestNG, SonarQube.

Release Stage
1. The software is deployed in a staging environment to simulate real-world conditions.

2. If everything checks out, the software is rolled out to production using deployment strategies like:

Blue-Green Deployment: Two identical environments switch traffic for a seamless update.
Canary Deployment: A small percentage of users get the new version first, ensuring safety.
Rolling Updates: The update is gradually pushed out to all users.
3. Common Tools: Docker, Kubernetes, Ansible, Helm, ArgoCD.


---

# How to Reduce the Cost of High Bandwidth Usage

> [!NOTE]
> Answer: Use caching and Amazon CloudFront, which is a CDN (Content Delivery Network).

### Story

Suppose a video is stored in an Amazon S3 bucket located in New York, and a user in a remote village in India tries to stream that video.
Because the data has to travel such a long distance, the bandwidth usage is high and latency increases.

### Solution

To reduce bandwidth costs and latency, the video should be transmitted from a location closer to the user.
By using a CDN like Amazon CloudFront, the video is cached at a nearby edge location. This ensures that when users in that region request the video, it is delivered quickly and efficiently.

![Video Streaming changing](![alt text](image.png))

### How It Works

``` CDNs maintain edge servers near users.

When a user requests a video for the first time, the CDN fetches it from the original server (e.g., the S3 bucket in New York).

The CDN then stores (caches) that video temporarily at the local edge server.

For subsequent requests, the CDN serves the video directly from the local cache, reducing both bandwidth and latency.

For better optimization, frequently accessed videos can be stored in a priority queue with timestamps and access frequency for smart caching decisions. ```

### Benefits

Reduced bandwidth costs

Lower latency and faster video delivery

Improved user experience

Optimized server load

---