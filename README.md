# ONLINE BOUTIQUE.
TURST THE PRODUCTS
import React, { useState } from 'react';

const componentTypes = {
  heading: 'Heading',
  text: 'Text',
  image: 'Image',
};

export default function App() {
  const [components, setComponents] = useState([]);

  const addComponent = (type) => {
    setComponents([
      ...components,
      { id: Date.now(), type, content: type === 'image' ? '' : `New ${type}` },
    ]);
  };

  const updateComponent = (id, newContent) => {
    setComponents(
      components.map((c) =>
        c.id === id ? { ...c, content: newContent } : c
      )
    );
  };

  return (
    <div className="min-h-screen p-4 bg-gray-100">
      <h1 className="text-3xl font-bold mb-4">Simple Websire Creator</h1>
      <div className="flex gap-2 mb-4">
        {Object.keys(componentTypes).map((type) => (
          <button
            key={type}
            onClick={() => addComponent(type)}
            className="bg-blue-500 hover:bg-blue-700 text-white px-4 py-2 rounded"
          >
            Add {componentTypes[type]}
          </button>
        ))}
      </div>

      <div className="bg-white p-4 rounded shadow">
        {components.map((comp) => (
          <div key={comp.id} className="mb-4">
            {comp.type === 'heading' && (
              <input
                type="text"
                className="text-2xl font-bold w-full border-b"
                value={comp.content}
                onChange={(e) =>
                  updateComponent(comp.id, e.target.value)
                }
              />
            )}
            {comp.type === 'text' && (
              <textarea
                className="w-full border p-2"
                value={comp.content}
                onChange={(e) =>
                  updateComponent(comp.id, e.target.value)
                }
              />
            )}
            {comp.type === 'image' && (
              <input
                type="text"
                className="w-full border p-2"
                placeholder="Image URL"
                value={comp.content}
                onChange={(e) =>
                  updateComponent(comp.id, e.target.value)
                }
              />
            )}
            {comp.type === 'image' && comp.content && (
              <img
                src={comp.content}
                alt="User content"
                className="mt-2 max-w-full h-auto"
              />
            )}
          </div>
        ))}
      </div>
    </div>
  );
}
