Unit Test


```javascript
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import { paste } from "@testing-library/user-event/dist/paste";
import ClipboardJS from "clipboard";
import React from "react";
import App from "./App";


it("Header should be rendered successfully", () => {
  render(<App />);
  const header = document.querySelector("header");
  expect(header).toBeDefined();

})

it("The emoji list should be rendered in a successfully", () => {
  render(<App />);
  const emojiRows = document.querySelectorAll(".component-emoji-result-row");
  const arr = [...emojiRows];

  expect(arr.length).toBe(20);
})


it("Filtering should work", () => {
  render(<App />);
  const input = document.querySelector("input");
  userEvent.type(input, "Smile")
  const emojiRows = document.querySelectorAll(".component-emoji-result-row");
  const arr = [...emojiRows];
  expect(arr.length).toBeLessThan(20);

})

it("emoji copying should work",()=>{
  render(<App />);
  const itemToBeClicked = document.querySelector(".component-emoji-results").firstChild;
  document.execCommand = jest.fn();
  userEvent.click(itemToBeClicked);
  expect(document.execCommand).toHaveBeenCalledWith("copy");
})

```