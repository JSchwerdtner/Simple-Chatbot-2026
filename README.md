1. Dependencies
  
Initialize your project and install the necessary libraries:
Bash command:
npm init -y
npm install @octokit/rest @octokit/webhooks dotenv openai

2. Environment Configuration

GITHUB_TOKEN=your_personal_access_token_or_app_token
OPENAI_API_KEY=your_openai_api_key
GITHUB_WEBHOOK_SECRET=your_secret_string
3. AI Logic

import { OpenAI } from 'openai';

const openai = new OpenAI();

export async function processPrompt(context) {
  const completion = await openai.chat.completions.create({
    model: "gpt-4o",
    messages: [{ role: "system", content: "You are a helpful GitHub assistant." },
               { role: "user", content: context }],
  });
  return completion.choices[0].message.content;
}


4. GitHub Integration

JavaScript:
import { Octokit } from '@octokit/rest';

const octokit = new Octokit({ auth: process.env.GITHUB_TOKEN });

export async function addComment(owner, repo, issueNumber, body) {
  await octokit.issues.createComment({
    owner,
    repo,
    issue_number: issueNumber,
    body,
  });
}
