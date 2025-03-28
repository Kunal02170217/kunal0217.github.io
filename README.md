import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";
import { Send } from "lucide-react";

export default function AIChatbot() {
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");

  const handleSend = async () => {
    if (!input.trim()) return;
    
    const userMessage = { text: input, sender: "user" };
    setMessages([...messages, userMessage]);
    setInput("");
    
    // Simulated AI response
    const aiMessage = { text: `AI says: ${input}`, sender: "ai" };
    setTimeout(() => setMessages([...messages, userMessage, aiMessage]), 1000);
  };

  return (
    <div className="flex flex-col items-center justify-center min-h-screen bg-gray-100 p-4">
      <Card className="w-full max-w-md shadow-xl">
        <CardContent className="p-4 space-y-4">
          <div className="h-96 overflow-y-auto bg-white p-4 rounded-lg shadow-sm">
            {messages.map((msg, index) => (
              <motion.div 
                key={index} 
                className={`p-2 rounded-lg my-1 max-w-xs ${msg.sender === "user" ? "bg-blue-500 text-white self-end ml-auto" : "bg-gray-200 text-black"}`}
                initial={{ opacity: 0, y: 10 }}
                animate={{ opacity: 1, y: 0 }}
                transition={{ duration: 0.3 }}
              >
                {msg.text}
              </motion.div>
            ))}
          </div>
          <div className="flex items-center space-x-2">
            <Input value={input} onChange={(e) => setInput(e.target.value)} placeholder="Type a message..." />
            <Button onClick={handleSend} className="bg-blue-600 text-white">
              <Send size={16} />
            </Button>
          </div>
        </CardContent>
      </Card>
    </div>
  );
}
