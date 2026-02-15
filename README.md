# AI Content Generator - OpenRouter Edition

An open-source AI-powered SEO content generator using OpenRouter API with **BYOAK (Bring Your Own API Key)** model. Users bring their own API keys, so you pay $0 for API costs!

Built with Next.js, React, and OpenRouter for maximum flexibility and minimum costs.

## 🚀 Quick Start

### Prerequisites
- Node.js 16+ and npm/yarn
- - An OpenRouter API key (get free at [openrouter.ai/keys](https://openrouter.ai/keys))
 
  - ### Installation
 
  - ```bash
    # Clone the repository
    git clone https://github.com/karanpuri1406-sys/ai-content-generator.git
    cd ai-content-generator

    # Install dependencies
    npm install

    # Start development server
    npm run dev
    ```

    Visit `http://localhost:3000` and add your OpenRouter API key in Settings.

    ---

    ## 📋 Features

    ### Core Features
    - ✨ **AI Content Generation** - Generate SEO-optimized blog posts using Claude, GPT-4, or other models
    - - 🔑 **User-Provided API Keys** - Users bring their own OpenRouter keys (zero API costs for you!)
      - - 🎨 **Multiple AI Models** - Auto-routing to best model or choose specific ones
        -   - OpenAI GPT-4
            -   - Anthropic Claude 3 (Opus, Sonnet)
                -   - Mistral Large
                    -   - Open-source models
                        - - 📝 **Content Editor** - Real-time preview and editing
                          - - 📥 **Multiple Export Formats** - Markdown, HTML, plain text
                            - - 💾 **Auto-Save** - Draft saving to browser storage
                              - - ⚡ **Fast Generation** - Optimized API calls for quick results
                               
                                - ### Advanced Features (Phase 2+)
                                - - 🖼️ **AI Image Generation** - Generate images with user's Stability AI or DALL-E key
                                  - - 📊 **Usage Analytics** - Track generation history (optional backend)
                                    - - 🔄 **Bulk Generation** - Generate multiple pieces at once
                                      - - 🎯 **Tone/Style Customization** - Professional, casual, technical, etc.
                                        - - 📱 **Responsive Design** - Works on desktop and mobile
                                          - - 🌙 **Dark Mode** - Easy on the eyes
                                           
                                            - ---

                                            ## 🏗️ Tech Stack

                                            ### Frontend
                                            - **Next.js 14** - React framework with SSR/SSG
                                            - - **React 18** - UI components
                                              - - **TailwindCSS** - Styling
                                                - - **React Query** - API state management
                                                  - - **React Markdown** - Render markdown content
                                                   
                                                    - ### Backend (Optional)
                                                    - - **Node.js + Express** OR **FastAPI** - API server
                                                      - - **PostgreSQL** - Database
                                                        - - **JWT** - Authentication
                                                         
                                                          - ### APIs
                                                          - - **OpenRouter API** - LLM routing and access
                                                            - - **Stability AI API** - Image generation (optional)
                                                             
                                                              - ### Deployment
                                                              - - **Vercel** - Frontend hosting (free tier)
                                                                - - **Railway/Render** - Backend hosting ($5+/month)
                                                                  - - **Supabase** - Database (free tier available)
                                                                   
                                                                    - ---

                                                                    ## 📁 Project Structure

                                                                    ```
                                                                    ai-content-generator/
                                                                    ├── app/
                                                                    │   ├── page.tsx              # Home page
                                                                    │   ├── layout.tsx            # Root layout
                                                                    │   └── api/                  # API routes (if needed)
                                                                    ├── components/
                                                                    │   ├── ContentGenerator.tsx  # Main generator component
                                                                    │   ├── SettingsPanel.tsx     # API key settings
                                                                    │   ├── ContentEditor.tsx     # Edit generated content
                                                                    │   └── ExportOptions.tsx     # Export functionality
                                                                    ├── hooks/
                                                                    │   ├── useContentGenerator.ts   # API call hook
                                                                    │   └── useLocalStorage.ts       # Browser storage hook
                                                                    ├── lib/
                                                                    │   ├── openrouter.ts        # OpenRouter API client
                                                                    │   └── constants.ts         # App constants
                                                                    ├── styles/
                                                                    │   └── globals.css          # Global styles
                                                                    └── public/                  # Static files
                                                                    ```

                                                                    ---

                                                                    ## 🔧 Implementation Guide

                                                                    ### Phase 1: Basic Setup (Week 1-2)

                                                                    #### 1. Create Next.js Project
                                                                    ```bash
                                                                    npx create-next-app@latest ai-content-generator --typescript --tailwind
                                                                    cd ai-content-generator
                                                                    npm install react-markdown react-query axios
                                                                    ```

                                                                    #### 2. Add SettingsPanel Component
                                                                    Create `components/SettingsPanel.tsx`:

                                                                    ```typescript
                                                                    import { useState } from 'react';

                                                                    export function SettingsPanel() {
                                                                      const [apiKey, setApiKey] = useState(
                                                                        localStorage.getItem('openrouter_key') || ''
                                                                      );

                                                                      const handleSaveKey = (e: React.FormEvent) => {
                                                                        e.preventDefault();
                                                                        if (!apiKey.trim()) {
                                                                          alert('Please enter a valid API key');
                                                                          return;
                                                                        }
                                                                        localStorage.setItem('openrouter_key', apiKey);
                                                                        alert('API Key saved securely in your browser!');
                                                                      };

                                                                      return (
                                                                        <div className="settings-panel p-6 bg-gray-900 rounded-lg">
                                                                          <h2 className="text-xl font-bold text-white mb-4">API Settings</h2>
                                                                          <form onSubmit={handleSaveKey}>
                                                                            <div className="mb-4">
                                                                              <label className="block text-gray-300 text-sm font-medium mb-2">
                                                                                OpenRouter API Key
                                                                              </label>
                                                                              <input
                                                                                type="password"
                                                                                value={apiKey}
                                                                                onChange={(e) => setApiKey(e.target.value)}
                                                                                placeholder="sk-or-..."
                                                                                className="w-full p-3 bg-gray-800 text-white border border-gray-700 rounded-lg focus:outline-none focus:border-blue-500"
                                                                              />
                                                                              <p className="text-xs text-gray-400 mt-2">
                                                                                Get your free API key at:{' '}
                                                                                <a
                                                                                  href="https://openrouter.ai/keys"
                                                                                  target="_blank"
                                                                                  rel="noopener noreferrer"
                                                                                  className="text-blue-400 hover:underline"
                                                                                >
                                                                                  openrouter.ai/keys
                                                                                </a>
                                                                              </p>
                                                                            </div>
                                                                            <button
                                                                              type="submit"
                                                                              className="w-full bg-blue-600 text-white py-2 rounded-lg font-medium hover:bg-blue-700 transition"
                                                                            >
                                                                              Save API Key
                                                                            </button>
                                                                          </form>
                                                                        </div>
                                                                      );
                                                                    }
                                                                    ```

                                                                    #### 3. Create Content Generator Hook
                                                                    Create `hooks/useContentGenerator.ts`:

                                                                    ```typescript
                                                                    import { useState } from 'react';

                                                                    export function useContentGenerator() {
                                                                      const [loading, setLoading] = useState(false);
                                                                      const [error, setError] = useState('');

                                                                      const generateContent = async (
                                                                        prompt: string,
                                                                        model: string = 'openrouter/auto'
                                                                      ) => {
                                                                        setLoading(true);
                                                                        setError('');

                                                                        try {
                                                                          const apiKey = localStorage.getItem('openrouter_key');

                                                                          if (!apiKey) {
                                                                            throw new Error('Please set your OpenRouter API key in settings');
                                                                          }

                                                                          const response = await fetch(
                                                                            'https://openrouter.ai/api/v1/chat/completions',
                                                                            {
                                                                              method: 'POST',
                                                                              headers: {
                                                                                'Content-Type': 'application/json',
                                                                                'Authorization': `Bearer ${apiKey}`,
                                                                                'HTTP-Referer': typeof window !== 'undefined' ? window.location.origin : '',
                                                                                'X-Title': 'AI Content Generator',
                                                                              },
                                                                              body: JSON.stringify({
                                                                                model: model,
                                                                                messages: [
                                                                                  {
                                                                                    role: 'system',
                                                                                    content: 'You are a professional SEO content writer. Create high-quality, engaging, well-structured content.',
                                                                                  },
                                                                                  {
                                                                                    role: 'user',
                                                                                    content: prompt,
                                                                                  },
                                                                                ],
                                                                                temperature: 0.7,
                                                                                max_tokens: 4000,
                                                                              }),
                                                                            }
                                                                          );

                                                                          if (!response.ok) {
                                                                            const errorData = await response.json();
                                                                            throw new Error(
                                                                              errorData.error?.message || 'Failed to generate content'
                                                                            );
                                                                          }

                                                                          const data = await response.json();
                                                                          return data.choices[0].message.content;
                                                                        } catch (err) {
                                                                          const message = err instanceof Error ? err.message : 'Unknown error';
                                                                          setError(message);
                                                                          throw err;
                                                                        } finally {
                                                                          setLoading(false);
                                                                        }
                                                                      };

                                                                      return { generateContent, loading, error };
                                                                    }
                                                                    ```

                                                                    #### 4. Create Main Generator Component
                                                                    Create `components/ContentGenerator.tsx`:

                                                                    ```typescript
                                                                    import { useState } from 'react';
                                                                    import { useContentGenerator } from '@/hooks/useContentGenerator';
                                                                    import ReactMarkdown from 'react-markdown';

                                                                    const AVAILABLE_MODELS = [
                                                                      { id: 'openrouter/auto', name: '🤖 Auto (Best Quality)' },
                                                                      { id: 'gpt-4', name: '✨ GPT-4' },
                                                                      { id: 'gpt-3.5-turbo', name: '⚡ GPT-3.5 Turbo (Fast)' },
                                                                      { id: 'claude-3-opus', name: '🧠 Claude 3 Opus' },
                                                                      { id: 'claude-3-sonnet', name: '💫 Claude 3 Sonnet' },
                                                                      { id: 'mistral-large', name: '🔥 Mistral Large' },
                                                                    ];

                                                                    export function ContentGenerator() {
                                                                      const [topic, setTopic] = useState('');
                                                                      const [selectedModel, setSelectedModel] = useState('openrouter/auto');
                                                                      const [generatedContent, setGeneratedContent] = useState('');
                                                                      const { generateContent, loading, error } = useContentGenerator();

                                                                      const handleGenerate = async (e: React.FormEvent) => {
                                                                        e.preventDefault();

                                                                        if (!topic.trim()) {
                                                                          alert('Please enter a topic');
                                                                          return;
                                                                        }

                                                                        const prompt = `Write a comprehensive, SEO-optimized blog post about: ${topic}

                                                                    Include:
                                                                    - Engaging introduction
                                                                    - Clear structure with H2 and H3 headings
                                                                    - Practical insights and tips
                                                                    - Real-world examples
                                                                    - Call-to-action at the end
                                                                    - Target word count: 2000 words
                                                                    - Use proper markdown formatting`;

                                                                        try {
                                                                          const content = await generateContent(prompt, selectedModel);
                                                                          setGeneratedContent(content);
                                                                        } catch (err) {
                                                                          console.error('Generation failed:', err);
                                                                        }
                                                                      };

                                                                      const copyToClipboard = () => {
                                                                        navigator.clipboard.writeText(generatedContent);
                                                                        alert('Content copied to clipboard!');
                                                                      };

                                                                      const downloadAsMarkdown = () => {
                                                                        const element = document.createElement('a');
                                                                        const file = new Blob([generatedContent], { type: 'text/markdown' });
                                                                        element.href = URL.createObjectURL(file);
                                                                        element.download = 'content.md';
                                                                        document.body.appendChild(element);
                                                                        element.click();
                                                                        document.body.removeChild(element);
                                                                      };

                                                                      return (
                                                                        <div className="max-w-6xl mx-auto p-6">
                                                                          <h1 className="text-4xl font-bold mb-8 text-white">AI Content Generator</h1>

                                                                          <div className="grid grid-cols-1 lg:grid-cols-2 gap-8">
                                                                            {/* Input Section */}
                                                                            <div>
                                                                              <form onSubmit={handleGenerate} className="bg-gray-800 p-6 rounded-lg">
                                                                                <div className="mb-4">
                                                                                  <label className="block text-gray-300 text-sm font-medium mb-2">
                                                                                    Content Topic
                                                                                  </label>
                                                                                  <textarea
                                                                                    value={topic}
                                                                                    onChange={(e) => setTopic(e.target.value)}
                                                                                    placeholder="Enter your content topic or brief description..."
                                                                                    className="w-full h-32 p-3 bg-gray-700 text-white border border-gray-600 rounded-lg focus:outline-none focus:border-blue-500"
                                                                                  />
                                                                                </div>

                                                                                <div className="mb-6">
                                                                                  <label className="block text-gray-300 text-sm font-medium mb-2">
                                                                                    AI Model
                                                                                  </label>
                                                                                  <select
                                                                                    value={selectedModel}
                                                                                    onChange={(e) => setSelectedModel(e.target.value)}
                                                                                    className="w-full p-3 bg-gray-700 text-white border border-gray-600 rounded-lg focus:outline-none focus:border-blue-500"
                                                                                  >
                                                                                    {AVAILABLE_MODELS.map(model => (
                                                                                      <option key={model.id} value={model.id}>
                                                                                        {model.name}
                                                                                      </option>
                                                                                    ))}
                                                                                  </select>
                                                                                  <p className="text-xs text-gray-400 mt-2">
                                                                                    Auto uses the best available model. Choose specific models for faster/cheaper results.
                                                                                  </p>
                                                                                </div>

                                                                                <button
                                                                                  type="submit"
                                                                                  disabled={loading}
                                                                                  className="w-full bg-blue-600 text-white py-3 rounded-lg font-medium hover:bg-blue-700 disabled:bg-gray-600 transition"
                                                                                >
                                                                                  {loading ? 'Generating... (this may take 30-60 seconds)' : 'Generate Content'}
                                                                                </button>
                                                                              </form>

                                                                              {error && (
                                                                                <div className="mt-4 bg-red-900 border border-red-700 text-red-200 p-4 rounded-lg">
                                                                                  <p className="font-semibold">Error:</p>
                                                                                  <p>{error}</p>
                                                                                </div>
                                                                              )}
                                                                            </div>

                                                                            {/* Output Section */}
                                                                            <div>
                                                                              {generatedContent ? (
                                                                                <div className="bg-gray-800 p-6 rounded-lg">
                                                                                  <div className="flex justify-between items-center mb-4">
                                                                                    <h2 className="text-xl font-bold text-white">Generated Content</h2>
                                                                                    <div className="flex gap-2">
                                                                                      <button
                                                                                        onClick={copyToClipboard}
                                                                                        className="text-sm bg-green-600 text-white px-3 py-2 rounded hover:bg-green-700 transition"
                                                                                      >
                                                                                        Copy
                                                                                      </button>
                                                                                      <button
                                                                                        onClick={downloadAsMarkdown}
                                                                                        className="text-sm bg-purple-600 text-white px-3 py-2 rounded hover:bg-purple-700 transition"
                                                                                      >
                                                                                        Download .md
                                                                                      </button>
                                                                                    </div>
                                                                                  </div>
                                                                                  <div className="bg-gray-700 p-4 rounded max-h-[600px] overflow-y-auto prose prose-invert max-w-none">
                                                                                    <ReactMarkdown>{generatedContent}</ReactMarkdown>
                                                                                  </div>
                                                                                </div>
                                                                              ) : (
                                                                                <div className="bg-gray-800 p-6 rounded-lg text-center text-gray-400 h-96 flex items-center justify-center">
                                                                                  <p>Generated content will appear here</p>
                                                                                </div>
                                                                              )}
                                                                            </div>
                                                                          </div>
                                                                        </div>
                                                                      );
                                                                    }
                                                                    ```

                                                                    ---

                                                                    ### Phase 2: Image Generation (Week 3)

                                                                    Create `components/ImageGenerator.tsx` to add image generation using user's Stability AI key.

                                                                    ### Phase 3: Advanced Features (Week 4+)

                                                                    - Save content history
                                                                    - - Create/manage projects
                                                                      - - Export to WordPress
                                                                        - - Team collaboration features
                                                                          - - Analytics dashboard
                                                                           
                                                                            - ---

                                                                            ## 🔐 Security Best Practices

                                                                            ✅ **DO:**
                                                                            - Store API keys in browser localStorage (user's device)
                                                                            - - Use HTTPS only for all requests
                                                                              - - Never log or expose API keys in errors
                                                                                - - Validate user input
                                                                                  - - Add rate limiting
                                                                                   
                                                                                    - ❌ **DON'T:**
                                                                                    - - Store API keys in your database (unless encrypted)
                                                                                      - - Send keys to third-party services
                                                                                        - - Use API keys in environment variables on frontend
                                                                                          - - Log API responses with sensitive data
                                                                                          - Share keys between users
                                                                                         
                                                                                          - ---

                                                                                          ## 💰 Monetization Options

                                                                                          1. **Open Source Free Tier**
                                                                                          2.    - Basic content generation
                                                                                                -    - Markdown export
                                                                                                     -    - No usage limits (user pays for their API key)
                                                                                                      
                                                                                                          - 2. **Premium Features (Optional)**
                                                                                                            3.    - Advanced analytics
                                                                                                                  -    - Image generation integration
                                                                                                                       -    - WordPress integration
                                                                                                                            -    - Team collaboration
                                                                                                                                 -    - Custom templates
                                                                                                                                  
                                                                                                                                      - 3. **Affiliate Program**
                                                                                                                                        4.    - Earn commission when users sign up for OpenRouter
                                                                                                                                              -    - Link to your referral
                                                                                                                                               
                                                                                                                                                   - 4. **SaaS Version**
                                                                                                                                                     5.    - Host for them with your own API key model
                                                                                                                                                           -    - Monthly subscription
                                                                                                                                                                -    - Usage-based pricing
                                                                                                                                                                 
                                                                                                                                                                     - ---
                                                                                                                                                                     
                                                                                                                                                                     ## 🚀 Deployment
                                                                                                                                                                     
                                                                                                                                                                     ### Deploy Frontend (Free)
                                                                                                                                                                     ```bash
                                                                                                                                                                     # Push to GitHub
                                                                                                                                                                     git push origin main

                                                                                                                                                                     # Connect Vercel
                                                                                                                                                                     # Visit vercel.com, import this repository
                                                                                                                                                                     # Deploy in one click
                                                                                                                                                                     ```
                                                                                                                                                                     
                                                                                                                                                                     ### Optional: Deploy Backend
                                                                                                                                                                     ```bash
                                                                                                                                                                     # Create account on Railway.app or Render.com
                                                                                                                                                                     # Connect GitHub repository
                                                                                                                                                                     # Add environment variables
                                                                                                                                                                     # Deploy
                                                                                                                                                                     ```
                                                                                                                                                                     
                                                                                                                                                                     ---
                                                                                                                                                                     
                                                                                                                                                                     ## 📚 Environment Variables
                                                                                                                                                                     
                                                                                                                                                                     Create `.env.local`:
                                                                                                                                                                     ```
                                                                                                                                                                     NEXT_PUBLIC_APP_NAME=AI Content Generator
                                                                                                                                                                     NEXT_PUBLIC_OPENROUTER_URL=https://openrouter.ai/api/v1/chat/completions

                                                                                                                                                                     # Backend only (if you add it)
                                                                                                                                                                     DATABASE_URL=postgresql://user:password@localhost/dbname
                                                                                                                                                                     JWT_SECRET=your-secret-key
                                                                                                                                                                     ```
                                                                                                                                                                     
                                                                                                                                                                     ---
                                                                                                                                                                     
                                                                                                                                                                     ## 🤝 Contributing
                                                                                                                                                                     
                                                                                                                                                                     Feel free to fork, modify, and use this project for personal or commercial use!
                                                                                                                                                                     
                                                                                                                                                                     ### Contributing Guidelines
                                                                                                                                                                     1. Fork the repository
                                                                                                                                                                     2. 2. Create a feature branch (`git checkout -b feature/amazing-feature`)
                                                                                                                                                                        3. 3. Commit changes (`git commit -m 'Add amazing feature'`)
                                                                                                                                                                           4. 4. Push to branch (`git push origin feature/amazing-feature`)
                                                                                                                                                                              5. 5. Open Pull Request
                                                                                                                                                                                
                                                                                                                                                                                 6. ---
                                                                                                                                                                                
                                                                                                                                                                                 7. ## 📄 License
                                                                                                                                                                                
                                                                                                                                                                                 8. This project is open source and available under the MIT License.
                                                                                                                                                                                
                                                                                                                                                                                 9. ---
                                                                                                                                                                                
                                                                                                                                                                                 10. ## 📞 Support
                                                                                                                                                                                
                                                                                                                                                                                 11. - 📖 [OpenRouter Documentation](https://openrouter.io/docs)
                                                                                                                                                                                     - - 🆘 [OpenRouter Support](https://openrouter.io/support)
                                                                                                                                                                                       - - 💬 GitHub Issues
                                                                                                                                                                                        
                                                                                                                                                                                         - ---
                                                                                                                                                                                         
                                                                                                                                                                                         ## 🎯 Roadmap
                                                                                                                                                                                         
                                                                                                                                                                                         - [x] Basic content generation
                                                                                                                                                                                         - [ ] - [ ] Image generation
                                                                                                                                                                                         - [ ] - [ ] WordPress integration
                                                                                                                                                                                         - [ ] - [ ] Usage analytics
                                                                                                                                                                                         - [ ] - [ ] Bulk generation
                                                                                                                                                                                         - [ ] - [ ] Team features
                                                                                                                                                                                         - [ ] - [ ] Mobile app
                                                                                                                                                                                         - [ ] - [ ] Browser extension
                                                                                                                                                                                        
                                                                                                                                                                                         - [ ] ---
                                                                                                                                                                                        
                                                                                                                                                                                         - [ ] ## ⭐ Show Your Support
                                                                                                                                                                                        
                                                                                                                                                                                         - [ ] If you find this project useful, please star it on GitHub!
                                                                                                                                                                                        
                                                                                                                                                                                         - [ ] ---
                                                                                                                                                                                        
                                                                                                                                                                                         - [ ] **Happy Content Generation! 🚀**
