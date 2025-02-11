---
id: useNavigation
title: useNavigation
---

**refine** uses [`React Router`](https://reactrouter.com/web/api/Hooks) and comes with all redirects out of the box. It allows you to manage your routing operations in refine. Using this hook, you can manage all the routing operations of your application very easily.

```tsx 
import { useNavigation } from "@pankod/refine";

const { create, edit, clone, show, list, push, replace, goBack } = useNavigation();
```

:::tip
`useNavigation` uses React Router's [useHistory](https://reactrouter.com/web/api/Hooks/usehistory) hook.
:::

### Usage

We will make a button for each method to use.

## List

Let's imagine that we have a post list and we want to be redirected to this page. To do this we will use the list hook.

```tsx  {3, 7, 12}
import {
    Button,
    useNavigation,
} from "@pankod/refine";

export const MyListButton = () => {
    const { list } = useNavigation();

    return (
        <Button
            onClick={(): void =>
                list("posts")
            }
        >
            Navigate to Post List Page
        </Button>
    );
};
```

### Create

If we want to go to the post creation page to create a new post, we can use the create hook.

```tsx  {3, 7, 12}
import {
    Button,
    useNavigation,
} from "@pankod/refine";

export const MyCreateButton = () => {
    const { create } = useNavigation();

    return (
        <Button
            onClick={(): void =>
                create("posts")
            }
        >
            Navigate to Create Page
        </Button>
    );
};
```

### Edit

Let's see what we should do if we want to go to the editing page of one of our posts.

```tsx  {3, 7, 12}
import {
    Button,
    useNavigation,
} from "@pankod/refine";

export const MyEditButton = () => {
    const { edit } = useNavigation();

    return (
        <Button
            onClick={(): void =>
                edit("posts", "1")
            }
        >
            Navigate to Edit Page
        </Button>
    );
};
```

We used the `edit` to navigate to the post edit page, but you can see the differences in using it. `edit` requires the id property from us and clicking the button will trigger the edit method of useNavigation and then redirect the app to `/posts/edit/1`

:::caution Attention
There is something we should pay attention to here. We need to give the `id` of which post we want to edit.
:::

:::tip
You can also give a `type` property to the methods. You can look here to see the [properties.](#properties)
:::

### Show

If you want to show the detail of your posts you can use show and you need `id` for show.

```tsx  {3, 7, 12}
import {
    Button,
    useNavigation,
} from "@pankod/refine";

export const MyShowButton = () => {
    const { show } = useNavigation();

    return (
        <Button
            onClick={(): void =>
                show("posts", "1")
            }
        >
            Navigate to Show Page
        </Button>
    );
};
```

:::caution Attention
There is something we should pay attention to here. We need to give the `id` of which post we want to show.
:::

:::tip
If you want to return to previous page. You can use `goBack` hook.
:::

### Clone

If we have the resources to clone a post and we want to go to this page, we will use `clone` with a record id.

```tsx  {3, 7, 12}
import {
    Button,
    useNavigation,
} from "@pankod/refine";

export const MyCloneButton = () => {
    const { clone } = useNavigation();

    return (
        <Button
            onClick={(): void =>
                clone("posts", "1")
            }
        >
            Navigate to Clone Page
        </Button>
    );
};
```

:::caution Attention
There is something we should pay attention to here. We need to give the `id` of which post we want to clone.
:::

### Push, Replace and GoBack

If we do not want to use the above methods and want to redirect ourselves, we should use `push` or `replace` methods and also we can use `goBack` to return to previous page. You can check out the differences between them [here](#return-values).

```tsx  {3, 7, 13, 20, 27}
import {
    Button,
    useNavigation,
} from "@pankod/refine";

export const MyHistoryButtons = () => {
    const { push, replace, goBack } = useNavigation();

    return (
        <>
            <Button
                onClick={(): void =>
                    push("posts")
                }
            >
                Push to posts Page
            </Button>
            <Button
                onClick={(): void =>
                    replace("posts")
                }
            >
                Replaces to posts Page
            </Button>
            <Button
                onClick={(): void =>
                    goBack()
                }
            >
                Go back to previous Page
            </Button>
        </>
    );
};
```

## API Reference

### Properties

| Property                                          | Description                                 | Type                      | Default  |
| ------------------------------------------------- | ------------------------------------------- | ------------------------- | -------- |
| resource <div className="required">Required</div> | Redirect the app to the given resource name | `string`                  |          |
| type                                              | It is React Router history types            | [HistoryType](#interface) | `"push"` |
| id                                                | It is used to append to the end of the path | `string`                  |          |

### Return values

| Property | Description                                     | Type                                                                         |
| -------- | ----------------------------------------------- | ---------------------------------------------------------------------------- |
| create   | Navigate to `create page` of your resource      | `(resource: string, type:` [HistoryType](#interface) `) => void `            |
| list     | Navigate to `list page` of your resource        | `(resource: string, type:` [HistoryType](#interface) `) => void`             |
| edit     | Navigate to `edit page` of your resource        | `(resource: string, type:` [HistoryType](#interface) `, id: string) => void` |
| clone    | Navigate to `clone page` of your resource       | `(resource: string, type:` [HistoryType](#interface) `, id: string) => void` |
| show     | Navigate to `show page` of your resource        | `(resource: string, type:` [HistoryType](#interface) `, id: string) => void` |
| push     | Pushes a new entry onto the history stack       | `(path: string, state?: unknown ) => void`                                   |
| replace  | Replaces the current entry on the history stack | `(path: string, state?: unknown ) => void`                                   |
| goBack   | Equivalent to go previous stack                 | `() => void`                                                                 |

#### Interface

```tsx title="History Type"
export type HistoryType = "push" | "replace";
```
