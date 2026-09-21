```ts
type VideoSource =
  | {
  type: "videoSourceBytes";
  bytes: Uint8Array;
}
  | {
  type: "videoSourceS3Location";
  location: S3Location;
};
```

Defined in: [src/types/media.ts:370](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/types/media.ts#L370)

Source for a video (Class version).