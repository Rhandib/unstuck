import React, { useState } from 'react';
import { Brain, Zap, Heart, Target, Lightbulb, CheckCircle } from 'lucide-react';

/**
 * BrainDouble component (updated)
 *
 * Adds a floating sloth background with color-shifting glow.
 */

export default function BrainDouble() {
  const [mode, setMode] = useState(null);
  const [step, setStep] = useState(0);

  const modes = {
    paralysis: {
      icon: Zap,
      title: "Task Paralysis",
      color: "bg-purple-500",
      steps: [
        {
          title: "Hey, I see you're stuck",
          message: "That overwhelming feeling? It's just your brain trying to protect you from uncertainty. But here's the truth: you don't need to see the whole staircase. You just need to take the first step.",
          action: "What's the absolute tiniest thing you could do right now? Not the 'right' thing. Just the smallest thing."
        },
        {
          title: "Pick ONE tiny action",
          message: "Open a file. Write one sentence. Send one email. Make one phone call. The magic isn't in picking the perfect task—it's in picking ANY task and doing it.",
          action: "I'm going to: _______",
          prompt: true
        },
        {
          title: "Set a 5-minute timer",
          message: "You heard me. FIVE minutes. That's it. You can do anything for 5 minutes. You're not committing to finishing. You're just committing to starting. Motion creates momentum.",
          action: "Timer set? Let's go! 🚀"
        },
        {
          title: "You're already winning",
          message: "Look at you. You broke the paralysis. The hardest part is over. You can stop now if you want... or you can keep going. But either way, you already proved you could start.",
          action: "Keep going or celebrate this win—both are valid."
        }
      ]
    },
    imposter: {
      icon: Heart,
      title: "Imposter Syndrome",
      color: "bg-rose-500",
      steps: [
        {
          title: "Let me tell you a secret",
          message: "That feeling that you're a fraud? It means you're growing. You're in new territory. You're challenging yourself. People who aren't growing don't feel like imposters—they feel comfortable.",
          action: "Discomfort = Growth. You're right where you need to be."
        },
        {
          title: "Evidence check",
          message: "Your brain is lying to you. Let's get factual. Name THREE things you've actually accomplished. Not 'big enough' accomplishments. Just things you DID that required skill, effort, or growth.",
          action: "Write them down. I'll wait.",
          prompt: true
        },
        {
          title: "The competence gap",
          message: "You know why you feel like an imposter? Because you can SEE how much there is to learn. That's not ignorance—that's wisdom. Beginners don't know what they don't know. You do. That means you're advancing.",
          action: "You're not behind. You're aware. There's a difference."
        },
        {
          title: "Do it 'badly'",
          message: "Permission granted: do this thing imperfectly. Do it as a learner, not an expert. Because that's what you are, and that's PERFECT for where you're at. Experts were once exactly where you are now.",
          action: "Go do the thing—as your authentic, still-learning self."
        }
      ]
    },
    avoidance: {
      icon: Target,
      title: "Avoidance Mode",
      color: "bg-blue-500",
      steps: [
        {
          title: "I see what you're doing",
          message: "Scrolling. Cleaning. 'Research.' Suddenly every other task seems urgent. Your brain is trying to protect you from something hard or uncomfortable. But avoidance doesn't make it go away—it makes it grow.",
          action: "What are you actually avoiding right now?"
        },
        {
          title: "Name the fear",
          message: "What's the worst thing that could happen if you do this task? Seriously. Say it out loud or write it down. Most fears lose power when you drag them into the light.",
          action: "My fear is: _______",
          prompt: true
        },
        {
          title: "Reframe it",
          message: "That thing you're avoiding? It's actually a door. On the other side is relief, growth, or progress. You don't have to want to do it. You just have to be willing to open the door.",
          action: "What's one benefit of doing this thing?"
        },
        {
          title: "The 2-minute deal",
          message: "Make a deal with yourself: work on it for just 2 minutes. If after 2 minutes you genuinely want to stop, you can. No judgment. But START the clock. Most times, you'll keep going.",
          action: "2 minutes. That's all I'm asking. Go."
        }
      ]
    }
  };

  const generalAdvice = [
    "You're capable of more than you think, but not in the way you think—it's not about doing everything perfectly. It's about doing things consistently, messily, imperfectly.",
    "Task paralysis isn't laziness. Imposter syndrome isn't truth. Avoidance isn't weakness. They're just your nervous system trying to keep you safe. Thank it, then do the thing anyway.",
    "Progress isn't linear. Some days you'll crush it. Some days survival is the win. Both count.",
    "You don't need motivation to start. You need to start to find motivation. Action comes first, feeling comes second.",
    "The person you're becoming is on the other side of the thing you're avoiding."
  ];

  const handleModeSelect = (modeKey) => {
    setMode(modeKey);
    setStep(0);
  };

  const handleNext = () => {
    if (step < modes[mode].steps.length - 1) {
      setStep(step + 1);
    } else {
      setMode(null);
      setStep(0);
    }
  };

  const handleReset = () => {
    setMode(null);
    setStep(0);
  };

  // Decorative floating sloths config
  const sloths = [
    { left: '5%', size: 80, delay: '0s', duration: '28s', rotate: '-10deg' },
    { left: '20%', size: 110, delay: '3s', duration: '34s', rotate: '6deg' },
    { left: '35%', size: 70, delay: '6s', duration: '30s', rotate: '-4deg' },
    { left: '55%', size: 95, delay: '1s', duration: '32s', rotate: '8deg' },
    { left: '70%', size: 120, delay: '5s', duration: '36s', rotate: '-6deg' },
    { left: '85%', size: 85, delay: '2s', duration: '30s', rotate: '4deg' },
  ];

  // Root layout when no mode selected (landing)
  if (!mode) {
    return (
      <div className="min-h-screen relative overflow-hidden bg-gradient-to-br from-indigo-900 via-purple-900 to-pink-900 p-8">
        {/* Floating Sloth Background Layer */}
        <div aria-hidden className="absolute inset-0 pointer-events-none">
          <div className="sloth-bg w-full h-full relative">
            {sloths.map((s, i) => (
              <span
                key={i}
                className="sloth-emoji"
                style={{
                  left: s.left,
                  width: s.size,
                  height: s.size,
                  fontSize: s.size * 0.6,
                  animationDelay: s.delay,
                  animationDuration: s.duration,
                  transform: `rotate(${s.rotate})`,
                }}
              >
                🦥
              </span>
            ))}
          </div>
        </div>

        <div className="max-w-4xl mx-auto relative z-10">
          <div className="text-center mb-12">
            <Brain className="w-16 h-16 text-white mx-auto mb-4" />
            <h1 className="text-4xl font-bold text-white mb-4">Your Brain Double</h1>
            <p className="text-xl text-purple-200">I'm here when things get hard. Pick what you're struggling with:</p>
          </div>

          <div className="grid md:grid-cols-3 gap-6 mb-12">
            {Object.entries(modes).map(([key, mode]) => {
              const Icon = mode.icon;
              return (
                <button
                  key={key}
                  onClick={() => handleModeSelect(key)}
                  className={`${mode.color} hover:opacity-90 transition-all transform hover:scale-105 p-8 rounded-2xl text-white shadow-2xl`}
                >
                  <Icon className="w-12 h-12 mx-auto mb-4" />
                  <h3 className="text-2xl font-bold">{mode.title}</h3>
                </button>
              );
            })}
          </div>

          <div className="bg-white/10 backdrop-blur-lg rounded-2xl p-8 border border-white/20">
            <div className="flex items-start gap-4 mb-6">
              <Lightbulb className="w-8 h-8 text-yellow-300 flex-shrink-0 mt-1" />
              <div>
                <h3 className="text-2xl font-bold text-white mb-4">Quick Reminders</h3>
                <ul className="space-y-3">
                  {generalAdvice.map((advice, i) => (
                    <li key={i} className="text-purple-100 leading-relaxed">
                      • {advice}
                    </li>
                  ))}
                </ul>
              </div>
            </div>
          </div>

          <div className="text-center mt-8 text-purple-200 italic">
            "You've got this. And if you don't right now, that's okay too. We'll figure it out together."
          </div>
        </div>

        {/* Styles for floating sloths and glow */}
        <style jsx>{`
          .sloth-bg { position: absolute; inset: 0; overflow: hidden; }
          .sloth-emoji {
            position: absolute;
            bottom: -20%;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            transform-origin: center;
            opacity: 0.85;
            filter: drop-shadow(0 10px 30px rgba(0,0,0,0.45)) saturate(150%);
            /* create a continuous hue-rotation glow */
            animation-name: floatUp, hueShift, sway;
            animation-timing-function: linear, ease-in-out, ease-in-out;
            animation-iteration-count: infinite, infinite, infinite;
            will-change: transform, filter;
            text-shadow:
              0 2px 8px rgba(255,255,255,0.06),
              0 6px 30px rgba(0,0,0,0.6);
          }

          /* vertical float */
          @keyframes floatUp {
            0% { transform: translateY(0) rotate(0deg); opacity: 0.9; }
            50% { opacity: 1; }
            100% { transform: translateY(-140vh) rotate(30deg); opacity: 0.85; }
          }

          /* side-to-side sway (subtle) */
          @keyframes sway {
            0% { transform: translateX(0) rotate(0deg); }
            50% { transform: translateX(10px) rotate(4deg); }
            100% { transform: translateX(0) rotate(0deg); }
          }

          /* hue shifting creates the glowing color changes */
          @keyframes hueShift {
            0% { filter: hue-rotate(0deg) drop-shadow(0 0 20px rgba(255,0,128,0.18)); }
            25% { filter: hue-rotate(90deg) drop-shadow(0 0 30px rgba(0,200,255,0.18)); }
            50% { filter: hue-rotate(180deg) drop-shadow(0 0 25px rgba(120,0,255,0.18)); }
            75% { filter: hue-rotate(270deg) drop-shadow(0 0 28px rgba(255,200,0,0.18)); }
            100% { filter: hue-rotate(360deg) drop-shadow(0 0 20px rgba(255,0,128,0.18)); }
          }

          /* prefers-reduced-motion: minimize animation */
          @media (prefers-reduced-motion: reduce) {
            .sloth-emoji {
              animation: none;
              opacity: 0.9;
              transform: translateY(-5vh) !important;
            }
          }

          /* ensure sloths are behind content */
          .sloth-emoji { z-index: 0; }
        `}</style>
      </div>
    );
  }

  // When mode selected - keep decorative background but subtle (smaller, fewer sloths)
  const currentMode = modes[mode];
  const currentStep = currentMode.steps[step];
  const Icon = currentMode.icon;

  return (
    <div className="min-h-screen relative overflow-hidden bg-gradient-to-br from-indigo-900 via-purple-900 to-pink-900 p-8">
      {/* Subtle floating sloths in mode view */}
      <div aria-hidden className="absolute inset-0 pointer-events-none">
        <div className="sloth-bg w-full h-full relative">
          {sloths.slice(0, 4).map((s, i) => (
            <span
              key={i}
              className="sloth-emoji"
              style={{
                left: s.left,
                width: s.size * 0.7,
                height: s.size * 0.7,
                fontSize: s.size * 0.7 * 0.6,
                animationDelay: s.delay,
                animationDuration: s.duration,
                transform: `rotate(${s.rotate})`,
                opacity: 0.7,
              }}
            >
              🦥
            </span>
          ))}
        </div>
      </div>

      <div className="max-w-3xl mx-auto relative z-10">
        <button
          onClick={handleReset}
          className="text-purple-200 hover:text-white mb-6 transition-colors"
        >
          ← Back to start
        </button>

        <div className="bg-white/10 backdrop-blur-lg rounded-3xl p-8 md:p-12 border border-white/20 shadow-2xl">
          <div className="flex items-center gap-4 mb-8">
            <div className={`${currentMode.color} p-4 rounded-full`}>
              <Icon className="w-8 h-8 text-white" />
            </div>
            <div>
              <h2 className="text-3xl font-bold text-white">{currentMode.title}</h2>
              <p className="text-purple-200">Step {step + 1} of {currentMode.steps.length}</p>
            </div>
          </div>

          <div className="mb-8">
            <h3 className="text-2xl font-bold text-white mb-4">{currentStep.title}</h3>
            <p className="text-xl text-purple-100 leading-relaxed mb-6">{currentStep.message}</p>
            
            {currentStep.prompt ? (
              <div className="bg-white/5 border-2 border-purple-400 rounded-xl p-6 mb-6">
                <p className="text-purple-200 mb-3">{currentStep.action}</p>
                <textarea 
                  className="w-full bg-white/10 border border-white/30 rounded-lg p-4 text-white placeholder-purple-300 focus:outline-none focus:ring-2 focus:ring-purple-400 min-h-24"
                  placeholder="Write it here... (this is just for you, nothing is saved)"
                />
              </div>
            ) : (
              <div className="bg-gradient-to-r from-purple-500/30 to-pink-500/30 rounded-xl p-6 border border-purple-400/50">
                <p className="text-lg font-semibold text-white">{currentStep.action}</p>
              </div>
            )}
          </div>

          <div className="flex gap-4">
            <button
              onClick={handleNext}
              className="flex-1 bg-gradient-to-r from-purple-500 to-pink-500 hover:from-purple-600 hover:to-pink-600 text-white font-bold py-4 px-8 rounded-xl transition-all transform hover:scale-105 shadow-lg"
            >
              {step < currentMode.steps.length - 1 ? 'Next →' : 'Done! ✓'}
            </button>
          </div>

          {step === currentMode.steps.length - 1 && (
            <div className="mt-6 text-center">
              <CheckCircle className="w-12 h-12 text-green-400 mx-auto mb-2" />
              <p className="text-purple-200 text-lg">You did it. Seriously. You showed up. That's everything.</p>
            </div>
          )}
        </div>

        <div className="mt-6 text-center text-purple-300 italic">
          "The version of you that's trying is already the version of you that's succeeding."
        </div>
      </div>

      {/* duplicate the same CSS rules here so they also apply to the mode view */}
      <style jsx>{`
        .sloth-bg { position: absolute; inset: 0; overflow: hidden; }
        .sloth-emoji {
          position: absolute;
          bottom: -20%;
          display: inline-flex;
          align-items: center;
          justify-content: center;
          transform-origin: center;
          opacity: 0.85;
          filter: drop-shadow(0 10px 30px rgba(0,0,0,0.45)) saturate(150%);
          animation-name: floatUp, hueShift, sway;
          animation-timing-function: linear, ease-in-out, ease-in-out;
          animation-iteration-count: infinite, infinite, infinite;
          will-change: transform, filter;
          text-shadow:
            0 2px 8px rgba(255,255,255,0.06),
            0 6px 30px rgba(0,0,0,0.6);
        }

        @keyframes floatUp {
          0% { transform: translateY(0) rotate(0deg); opacity: 0.9; }
          50% { opacity: 1; }
          100% { transform: translateY(-140vh) rotate(30deg); opacity: 0.85; }
        }

        @keyframes sway {
          0% { transform: translateX(0) rotate(0deg); }
          50% { transform: translateX(10px) rotate(4deg); }
          100% { transform: translateX(0) rotate(0deg); }
        }

        @keyframes hueShift {
          0% { filter: hue-rotate(0deg) drop-shadow(0 0 20px rgba(255,0,128,0.18)); }
          25% { filter: hue-rotate(90deg) drop-shadow(0 0 30px rgba(0,200,255,0.18)); }
          50% { filter: hue-rotate(180deg) drop-shadow(0 0 25px rgba(120,0,255,0.18)); }
          75% { filter: hue-rotate(270deg) drop-shadow(0 0 28px rgba(255,200,0,0.18)); }
          100% { filter: hue-rotate(360deg) drop-shadow(0 0 20px rgba(255,0,128,0.18)); }
        }

        @media (prefers-reduced-motion: reduce) {
          .sloth-emoji {
            animation: none;
            opacity: 0.9;
            transform: translateY(-5vh) !important;
          }
        }

        .sloth-emoji { z-index: 0; }
      `}</style>
    </div>
  );
}
