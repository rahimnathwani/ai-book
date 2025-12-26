# Complete Chapter Outline: AI Agents for the IT Professional

---

## Part I: Foundations — Understanding the AI Landscape

### Chapter 1: The AI You Already Know
*Establishing context for readers who have used AI but haven't built with it*

1.1 Classification models: The workhorse of traditional AI
- CNNs for image classification (e.g., "What type of bird is this?")
- RNNs/LSTMs for sequence classification (e.g., sentiment analysis)
- What these are: Models that map inputs to predefined categories
- What these are not: Models that create new content or make decisions

1.2 Beyond classification: Other recognition models
- Object detection: Finding bounding boxes and multiple objects
- Segmentation: Pixel-level classification
- OCR: Extracting text from images
- What these are: Models that identify and locate things in data
- What these are not: Models that understand meaning or context deeply

1.3 How AI has traditionally been integrated into software
- AI as an external API call
- Send data in, get data back
- Examples: Image → text (OCR), image → boolean (hotdog detector), text → class (spam filter)
- The software remains "normal" — deterministic, predictable, in control

---

### Chapter 2: The Generative Revolution
*Understanding what makes modern AI different*

2.1 What generative models actually do
- The core insight: Prediction as generation
- Diffusion models: Predicting and removing noise to create images
- LLMs: Predicting the next token to generate text
- What these are: Models that create new content by learning patterns
- What these are not: Databases that retrieve stored information

2.2 How LLMs are trained
- Pretraining: Learning language from massive text corpora
- Fine-tuning: Specializing for specific tasks (e.g., instruction following)
- RLHF: Reinforcement learning from human feedback
- Why this matters: Understanding training helps you understand capabilities and limitations

2.3 The context window: An LLM's working memory
- What tokens are (roughly ¾ of a word)
- Current context window sizes (128K to 1M+ tokens)
- What fits in context vs. what doesn't
- What this is: The complete "awareness" the model has for any given response
- What this is not: Long-term memory or persistent knowledge

2.4 System prompts vs. user prompts
- System prompt: The agent's job description and training manual
- User prompt: The specific work request
- How they interact and persist
- What these are: Configuration and instruction mechanisms
- What these are not: Programming in the traditional sense

---

## Part II: From Workflows to Agents — A Critical Distinction

### Chapter 3: AI-Powered Workflows
*The intermediate step most teams should start with*

3.1 What workflows are
- Traditional software with AI components
- The software remains in control
- AI provides outputs; software decides what to do with them
- Example: Spam filter returns 75% confidence; software applies 80% threshold

3.2 Common workflow patterns
- Classification and routing (spam, support ticket categorization)
- Extraction and transformation (parsing documents, normalizing data)
- Generation with templates (drafting responses, creating reports)
- Scoring and ranking (lead scoring, content moderation)

3.3 The power and limitations of workflows
- Predictable, auditable, controllable
- Easy to test and monitor
- Limited by the imagination of the designer
- Cannot adapt to unexpected situations

3.4 What workflows are and are not
- What they are: Deterministic processes that use AI for specific subtasks
- What they are not: Systems that can reason about novel problems or choose their own approach

---

### Chapter 4: Enter the Agent
*The fundamental shift in how AI systems operate*

4.1 The defining characteristic of agents
- The AI model decides which tools to call
- Control shifts from software to model
- The agent pursues goals, not just executes instructions

4.2 The agentic loop
- Observe the current state
- Decide what to do
- Take an action (call a tool)
- Observe the result
- Repeat until task complete (or limits reached)
- What this is: An iterative reasoning and acting cycle
- What this is not: A single API call or linear process

4.3 Tools: The agent's hands
- Tools as functions the agent can call
- Common tool types: File operations, web search, API calls, code execution
- The agent reads tool descriptions to decide which to use
- What tools are: Capabilities you grant to the agent
- What tools are not: Guaranteed actions (the agent chooses whether to use them)

4.4 Workflows vs. agents: When to use which
- Workflows: When you know exactly what needs to happen
- Agents: When the path to the goal requires reasoning and adaptation
- The hybrid approach: Agents that invoke workflows

---

### Chapter 5: Agent Harnesses
*The software that makes agents practical*

5.1 What an agent harness does
- Manages the agentic loop
- Provides tool infrastructure
- Handles context window management
- Provides user interface for interaction
- Manages security and sandboxing

5.2 The evolution of consumer AI interfaces
- ChatGPT and Claude web UIs as early examples
- Initially: Simple wrappers for LLMs with no tools
- Now: Full agent harnesses with web search, code execution, file access
- Example: Asking for today's weather — tool use vs. hallucination

5.3 The current state of the art: CLI-based agent harnesses
- Claude Code CLI
- Codex CLI
- Gemini CLI
- Cursor (and cursor-agent mode)
- Why CLI? Access to filesystem, command execution, development workflows

5.4 Why coding dominates current agent use
- Agents have access to read/edit files and run commands
- Code is text — LLMs are good at text
- Immediate feedback loop: Run code, see results
- Rich tool ecosystem already exists (compilers, linters, test frameworks)

5.5 What harnesses are and are not
- What they are: Infrastructure that turns an LLM into a practical agent
- What they are not: The intelligence itself (that's the model)

---

## Part III: Building with Agents — Practical Considerations

### Chapter 6: The General-Purpose Agent Hiding in Plain Sight
*Recognizing that coding agents are actually universal agents*

6.1 Claude Code et al. are not just for code
- They're general-purpose agents with coding-focused defaults
- Any task that can be accomplished via tools is fair game

6.2 Extending agents with custom tools
- Adding access to email systems
- Connecting to HR systems, CRMs, databases
- Integrating with communication platforms (Slack, Teams)

6.3 Example: The manager review reminder system
- Agent accesses HR system to find overdue reviews
- Agent accesses email to send reminders
- Multi-step process executed patiently and systematically
- What you provide: Tools and instructions
- What the agent provides: Reasoning about how to accomplish the goal

6.4 The key insight
- If the information is available via API, and the actions are available via API, the agent can probably do the task
- The agent's value: Reasoning through multi-step processes, handling variations, adapting to what it finds

---

### Chapter 7: Tools and the Model Context Protocol
*Designing the capabilities you give to agents*

7.1 Tool design is API design (with a twist)
- Clear, unambiguous names and descriptions
- Well-documented parameters
- Concise, informative return values
- Remember: Return values consume context window

7.2 The Model Context Protocol (MCP)
- A standardized interface for agent tools
- The "USB standard" for agent capabilities
- Build once, use with any MCP-compatible harness
- MCP servers: Exposing tools and resources

7.3 Common MCP servers and patterns
- Filesystem access
- Database queries
- API wrappers for common services
- Custom business logic

7.4 Building your own MCP servers
- When to build vs. use existing
- Basic architecture and implementation
- Testing and debugging tools

7.5 What good tool design is and is not
- What it is: Clear contracts that help the agent make good decisions
- What it is not: Trying to constrain the agent's reasoning through tool design

---

### Chapter 8: Instructing Agents Effectively
*The art and science of prompt engineering*

8.1 Why instruction quality matters enormously
- Unlike code: You write natural language, not precise syntax
- Vague instructions produce vague results
- Example: "Clean up this data" vs. specific transformation rules

8.2 Principles of effective agent instructions
- Be specific about the goal and success criteria
- Provide context the agent needs
- Specify constraints and boundaries
- Include examples when helpful
- Anticipate edge cases

8.3 Structured outputs for reliable handoffs
- Requesting JSON responses
- Schema constraints
- Why structure matters for agent-to-software interfaces

8.4 The difference between prompting and programming
- What prompting is: Clear communication of intent and constraints
- What prompting is not: Precise control over execution path

---

### Chapter 9: When Agents Should Write Code Instead
*Knowing the limits of in-context reasoning*

9.1 The cognitive load principle
- Just as you wouldn't ask a human to sum 10,000 numbers in their head
- Some tasks are better done by deterministic code
- The agent's job: Write the code, not do the computation

9.2 Tasks where agents should write code
- Data transformations (joining CSVs, aggregations)
- Numerical computations
- Repetitive operations over large datasets
- Anything requiring precision over creativity

9.3 Tasks where agents should reason directly
- Novel problem-solving
- Situations requiring judgment
- Tasks with ambiguity that requires interpretation
- Creative work

9.4 The hybrid pattern
- Agent reasons about approach
- Agent writes code to execute
- Agent interprets results
- Agent decides next steps

---

### Chapter 10: RAG and Knowledge Access
*Giving agents access to information they weren't trained on*

10.1 The knowledge problem
- LLMs only know training data + context window
- Your proprietary information isn't in training data
- Context windows are limited

10.2 Retrieval-Augmented Generation (RAG)
- Search relevant documents before generating
- Inject found information into context
- Answer based on retrieved knowledge
- Example: Customer support agent searching knowledge base

10.3 Implementing RAG
- Document chunking and embedding
- Vector databases and similarity search
- Prompt construction with retrieved context
- Handling conflicting or incomplete information

10.4 RAG vs. fine-tuning vs. better prompts
- Start with better prompts (often sufficient)
- Add RAG for proprietary/current knowledge
- Consider fine-tuning only for behavior changes or cost optimization
- What RAG is: A retrieval pattern that augments the model's knowledge
- What RAG is not: A replacement for good prompting or appropriate model selection

---

### Chapter 11: Handling Agent Mistakes
*Building systems that account for imperfection*

11.1 The fundamental reality: Agents make mistakes
- Hallucination is inherent to LLMs
- Confident incorrectness
- Misunderstanding instructions
- Taking wrong turns in multi-step processes

11.2 This is different from traditional software
- Traditional bugs: The code does what you wrote (wrongly)
- Agent errors: The agent reasons incorrectly despite good instructions
- Non-determinism: Same input may produce different outputs

11.3 Strategies for managing mistakes
- Have agents explain their reasoning (chain of thought)
- Ask agents to verify their own work
- Use a second agent to review the first
- Build in human checkpoints for high-stakes decisions
- Design for reversibility where possible

11.4 What error handling is and is not
- What it is: Accepting imperfection and designing around it
- What it is not: Expecting to achieve 100% reliability through better prompts

---

### Chapter 12: Human-in-the-Loop Patterns
*Keeping humans appropriately involved*

12.1 The autonomy spectrum
- AI-assisted: Human does work, AI provides suggestions
- AI-drafted: AI does first pass, human reviews and edits
- AI-executed with approval: AI completes task, human approves before effect
- Fully autonomous: AI acts without human intervention

12.2 Choosing the right level of autonomy
- Stakes: What's the cost of an error?
- Reversibility: Can mistakes be undone?
- Confidence: How reliable is the system for this task?
- Volume: Is human review practical at this scale?

12.3 Implementing approval workflows
- Confirmation prompts before tool execution
- Review queues for batched operations
- Escalation paths for uncertain situations
- Audit trails for all agent actions

12.4 Example: The email campaign with review
- Agent drafts all 50 reminder emails
- Emails queued for human review
- Human approves, edits, or rejects each
- Approved emails sent automatically

---

### Chapter 13: Security, Sandboxing, and Least Privilege
*Protecting your systems from your agents*

13.1 The power and danger of tool access
- Tools = ability to take real-world actions
- Read files, make API calls, send messages, execute code
- An agent with too much access is a significant risk

13.2 Sandboxing and isolation
- Containers and VMs for agent execution
- Network isolation
- Filesystem restrictions
- Resource limits (CPU, memory, time)

13.3 The principle of least privilege
- Grant only the tools needed for the task
- Code review agent doesn't need email access
- Email agent doesn't need database delete permissions
- Separate agents for separate concerns

13.4 Authentication and authorization
- How agents authenticate to external services
- Token management and rotation
- Audit logging for compliance
- Revoking access when needed

13.5 What security means for agents
- What it is: Defense in depth, assuming the agent may misbehave
- What it is not: Trusting the agent to respect boundaries it can technically bypass

---

### Chapter 14: Cost, Latency, and Operational Concerns
*The practical economics of agent systems*

14.1 Understanding costs
- Per-token pricing (input and output)
- A complex task may involve dozens of LLM calls
- Example costs: $0.50-5.00 for a 5-minute agent task
- Comparing to human time and traditional compute

14.2 Managing costs
- Choosing appropriate models for tasks
- Efficient prompt design
- Caching where possible
- Setting budget limits and alerts

14.3 Latency considerations
- 1-30 seconds per LLM call (depending on response length)
- Multi-step tasks compound latency
- User experience implications
- Async patterns for long-running tasks

14.4 When the economics don't work
- High-volume, low-value tasks
- Tasks requiring very low latency
- Situations where traditional software is more cost-effective

---

### Chapter 15: Observability and Debugging
*Understanding what your agent is thinking*

15.1 The debugging challenge
- Traditional: Logs, stack traces, deterministic replay
- Agents: Non-deterministic reasoning, implicit decisions
- Debugging an agent is like debugging a human collaborator

15.2 What to capture
- Full conversation logs (including system prompts)
- Tool calls and their results
- Token usage and timing
- Model's reasoning (when using chain of thought)

15.3 Tools and techniques
- Conversation viewers in agent harnesses
- Custom logging infrastructure
- Replay and analysis tools
- A/B testing different prompts or configurations

15.4 Common failure patterns and how to identify them
- Context window overflow (agent "forgets" earlier information)
- Tool misuse (wrong tool for the job)
- Instruction misinterpretation
- Hallucination in reasoning steps

---

### Chapter 16: Testing and Evaluation
*How do you know if your agent system works?*

16.1 The testing challenge
- Non-deterministic outputs
- "Correct" may be subjective
- Traditional unit tests don't fully apply

16.2 Evaluation approaches
- Test on held-out example sets
- Manual review of outputs
- LLM-as-judge: Second model evaluates first
- Specific metrics: Completion rate, cost, error types

16.3 Building evaluation datasets
- Representative examples of real tasks
- Edge cases and failure modes
- Golden outputs for comparison

16.4 Continuous evaluation
- Monitoring production behavior
- Catching regression when prompts or models change
- Feedback loops from users

16.5 What testing means for agents
- What it is: Systematic evaluation accepting some uncertainty
- What it is not: Achieving the deterministic confidence of traditional software testing

---

## Part IV: Putting It All Together

### Chapter 17: Multi-Agent Systems
*When one agent isn't enough*

17.1 Why multiple agents?
- Separation of concerns
- Different capabilities or access levels
- Adversarial patterns (worker + critic)
- Specialized expertise

17.2 Common patterns
- Planner + workers: One agent breaks down tasks, others execute
- Reviewer pattern: One agent does work, another critiques
- Escalation: Simple agent handles routine, complex agent handles exceptions
- Pipeline: Each agent handles one stage

17.3 Coordination challenges
- Shared context and state
- Conflict resolution
- Resource management
- Debugging distributed reasoning

17.4 When multi-agent is and isn't appropriate
- What it's good for: Complex tasks with clear subtask boundaries
- What it's not: A solution to single-agent reliability problems

---

### Chapter 18: What Agents Are Bad At (Today)
*Knowing the limitations*

18.1 Tasks requiring precise computation
- Numerical calculations
- Exact string manipulation
- Anything where "close" isn't good enough
- Solution: Have the agent write code instead

18.2 Tasks requiring unavailable knowledge
- Information not in training data
- Information that can't be retrieved via tools
- Real-time data without appropriate tool access

18.3 Tasks requiring physical world interaction
- Agents operate in the digital realm
- Physical automation requires different systems
- Agents can orchestrate but not manipulate

18.4 Very long time horizon tasks
- Context window limits
- Maintaining coherence over hours/days
- State management challenges

18.5 Zero-error-tolerance tasks
- Critical systems where any mistake is unacceptable
- Agents cannot guarantee perfection
- Traditional software may be more appropriate

18.6 Tasks with vague success criteria
- "Make it better" is hard to execute
- Clear goals produce better results
- Agents can't read your mind

---

### Chapter 19: The Build vs. Configure Decision
*Choosing your approach*

19.1 Configuring existing harnesses
- Claude Code, Cursor, etc. with custom tools
- Faster time to value
- Leverage existing infrastructure
- Limited by harness capabilities

19.2 Building from scratch
- Direct API integration (OpenAI, Anthropic, etc.)
- Frameworks (LangChain, LlamaIndex, etc.)
- Maximum flexibility
- Significant development effort

19.3 When to configure
- Most practical business applications
- Prototyping and experimentation
- When existing harnesses meet requirements
- When time to value matters

19.4 When to build
- Building a product
- Deep customization requirements
- Specific UX needs
- Scale or performance requirements existing harnesses can't meet

---

### Chapter 20: Getting Started — A Practical Path
*From experimentation to production*

20.1 Phase 1: Personal experimentation
- Use Claude Code or similar for your own tasks
- Learn how to instruct an agent effectively
- Understand capabilities and limitations firsthand
- Build intuition through direct experience

20.2 Phase 2: Custom tool development
- Identify repetitive tasks in your work
- Build MCP servers for your internal systems
- Start with read-only tools (safer)
- Gradually add write capabilities

20.3 Phase 3: Team workflows
- Document successful patterns
- Create clear instructions and constraints
- Establish review and approval processes
- Train team members

20.4 Phase 4: Production systems
- Build monitoring and alerting
- Implement proper security controls
- Establish cost management
- Create feedback loops for improvement

20.5 Phase 5: Custom infrastructure (if needed)
- Only after proving value with existing tools
- Clear requirements that justify the investment
- Build on lessons learned from earlier phases

---

## Appendices

### Appendix A: Worked Example — Building an Expense Report Processor
- Requirements gathering
- Tool design
- Instruction development
- Testing and refinement
- Production deployment

### Appendix B: Worked Example — Automated Onboarding Documentation
- Integrating with HR systems
- Generating personalized materials
- Review workflow implementation
- Measuring success

### Appendix C: Comparison of Major Agent Harnesses
- Claude Code
- Codex CLI
- Gemini CLI
- Cursor
- Feature comparison matrix
- Use case recommendations

### Appendix D: MCP Server Reference
- Common public MCP servers
- Building a basic MCP server (step-by-step)
- Testing and debugging MCP servers
- Security considerations

### Appendix E: Prompt Patterns That Work
- Task decomposition prompts
- Verification prompts
- Error handling prompts
- Output formatting prompts
- Examples with commentary

### Appendix F: Glossary of Terms
