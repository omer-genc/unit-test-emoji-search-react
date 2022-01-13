Unit Test


```javascript
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import { paste } from "@testing-library/user-event/dist/paste";
import ClipboardJS from "clipboard";
import React from "react";
import App from "./App";


it("header should be rendered", () => {
  render(<App />);
  const header = document.querySelector("header");
  expect(header).toBeDefined();

})

it("should be emoji list item 20", () => {
  render(<App />);
  const emojiRows = document.querySelectorAll(".component-emoji-result-row");
  const arr = [...emojiRows];

  expect(arr.length).toBe(20);
})


it("search emoji", () => {
  render(<App />);
  const input = document.querySelector("input");
  userEvent.type(input, "Smile")
  const emojiRows = document.querySelectorAll(".component-emoji-result-row");
  const arr = [...emojiRows];
  expect(arr.length).toBeLessThan(20);

})

it("click and copy emoji",()=>{
  render(<App />);
  const itemToBeClicked = document.querySelector(".component-emoji-results").firstChild;
  document.execCommand = jest.fn();
  userEvent.click(itemToBeClicked);
  expect(document.execCommand).toHaveBeenCalledWith("copy");
})

```