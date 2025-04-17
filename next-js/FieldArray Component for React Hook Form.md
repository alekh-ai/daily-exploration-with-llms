# FieldArray Component for React Hook Form

## Overview

The `FieldArray` component is a type-safe wrapper for React Hook Form's `useFieldArray` hook. It provides a flexible solution for managing dynamic arrays of form fields with proper TypeScript support.

## Installation

Ensure you have the following dependencies installed:

```bash
npm install react-hook-form
```

## Usage

```tsx
import { useForm } from "react-hook-form";
import { FieldArray } from "@/components/FieldArray";

// Define your form type
type FormValues = {
  items: { name: string; quantity: number }[];
};

export default function MyForm() {
  const { control, handleSubmit } = useForm<FormValues>({
    defaultValues: {
      items: [{ name: "", quantity: 0 }]
    }
  });

  return (
    <form onSubmit={handleSubmit(data => console.log(data))}>
      <FieldArray
        control={control}
        name="items"
        defaultItem={{ name: "", quantity: 0 }}
        render={({ fields, remove }) => (
          <>
            {fields.map((field, index) => (
              <div key={field.id}>
                {/* Your field inputs go here */}
                <button type="button" onClick={() => remove(index)}>
                  Remove
                </button>
              </div>
            ))}
          </>
        )}
      />
      
      <button type="submit">Submit</button>
    </form>
  );
}
```

## Props

The component accepts the following props:

| Prop | Type | Description |
|------|------|-------------|
| `control` | `Control<T>` | The control object from React Hook Form |
| `name` | `string` | Field array name in the form |
| `render` | `Function` | Render prop function that receives fields, append, and remove |
| `defaultItem` | `any` | Default item to add when clicking the add button |
| `className` | `string` | Optional CSS class name for the container |
| `addButtonText` | `string` | Optional text for the add button |

## TypeScript Implementation

```tsx
"use client";

import React from "react";
import { useFieldArray, Control, FieldValues, UseFieldArrayReturn } from "react-hook-form";
import { Button } from "@/components/ui/button";
import { cn } from "@/lib/utils";

// Define a generic type parameter T
type FieldArrayProps<T extends FieldValues> = {
  control: Control<T>;
  name: string;
  render: (props: {
    fields: UseFieldArrayReturn<T>['fields'];
    append: UseFieldArrayReturn<T>['append'];
    remove: UseFieldArrayReturn<T>['remove'];
  }) => React.ReactNode;
  defaultItem: T[keyof T];
  className?: string;
  addButtonText?: string;
};

export function FieldArray<T extends FieldValues>({
  control,
  name,
  render,
  defaultItem,
  className = "space-y-4",
  addButtonText = "Add Item",
}: FieldArrayProps<T>) {
  const { fields, append, remove } = useFieldArray({
    control,
    name,
  });

  return (
    <div className={cn(className)}>
      {render({ fields, append, remove })}
      
      <Button
        type="button"
        variant="secondary"
        onClick={() => append(defaultItem)}
      >
        {addButtonText}
      </Button>
    </div>
  );
}
```

## Key Implementation Details

### Generic Type Parameter

The component uses a generic type parameter `T extends FieldValues` to ensure type safety throughout the component. This allows TypeScript to properly check the types of fields, control, and default items.

### Render Prop Pattern

The `render` prop follows the render prop pattern, providing:

- `fields`: Array of form fields with IDs and values
- `append`: Function to add new items to the array
- `remove`: Function to remove items from the array by index

This pattern gives users full control over how fields are rendered while maintaining type safety.

### Default Add Button

The component includes a default "Add Item" button that appends the provided `defaultItem` to the array. The button text can be customized using the `addButtonText` prop.

## Why Use This Component?

- **Type Safety**: Eliminates the need for `any` types in your form code
- **Reusability**: Create consistent field arrays across your application
- **Flexibility**: The render prop pattern allows for custom rendering while maintaining functionality
- **Simplicity**: Encapsulates the complexity of `useFieldArray` behind a clean API
