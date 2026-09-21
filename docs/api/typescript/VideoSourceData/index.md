```ts
type VideoSourceData =
  | {
  bytes: Uint8Array;
}
  | {
  location: S3LocationData;
};
```

Defined in: [src/types/media.ts:365](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/types/media.ts#L365)

Source for a video (Data version).