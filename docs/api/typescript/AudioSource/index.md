```ts
type AudioSource =
  | {
  type: "audioSourceBytes";
  bytes: Uint8Array;
}
  | {
  type: "audioSourceS3Location";
  location: S3Location;
};
```

Defined in: [src/types/media.ts:145](https://github.com/strands-agents/harness-sdk/blob/f28adcd83d480d3a2edc76db0c583e8a26f50a63/strands-ts/src/types/media.ts#L145)

Source for an audio block (Class version).