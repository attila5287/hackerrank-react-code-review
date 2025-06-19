# Solution 1: flat state votes and vote types

```JS
import { useState } from "react";
import "./App.css";

const App = () => {
  const [items, setItems] = useState(
    ["Readability", "Performance", "Security", "Documentation", "Testing"].map(
      (name) => ({ name, upvotes: 0, downvotes: 0 })
    )
  );

  const handleVote = (aspect: string, type: "upvotes" | "downvotes") => {
    setItems((prev) =>
      prev.map((item) =>
        item.name === aspect  
          ? { ...item, [type]: item[type] + 1 }
          : { ...item, [type]: item[type] }
      )
    );
  };

  return (
    <div style={{ padding: 10 }}>
      <h2>Code Review Feedback</h2>
      {items.map((item) => (
        <div
          key={item.name}
          style={{
            margin: "10px 0",
            padding: 10,
            border: "1px solid #ccc",
            borderRadius: 4,
          }}
        >
          <h3 className="margin-zero">{item.name}</h3>
          <button
            data-type="upvotes"
            data-aspect={item.name}
            onClick={(e) => {
              const aspect = (e.target as HTMLButtonElement).dataset.aspect;
              const type = (e.target as HTMLButtonElement).dataset.type;
              console.log(aspect, type);
              handleVote(aspect as string, type as "upvotes" | "downvotes");
            }}
          >
            <i className="fa-solid fa-thumbs-up"></i>
            Upvote
          </button>
          <span> {item.upvotes} </span>
          <button
            data-type="downvotes"
            data-aspect={item.name}
            onClick={(e) => {
              const aspect = (e.target as HTMLButtonElement).dataset.aspect;
              const type = (e.target as HTMLButtonElement).dataset.type;
              console.log(aspect, type);
              handleVote(aspect as string, type as "upvotes" | "downvotes");
            }}
          >
            <i className="fa-solid fa-thumbs-down"></i>
            Downvote
          </button>
          <span> {item.downvotes} </span>
        </div>
      ))}
    </div>
  );
};

export default App;

```