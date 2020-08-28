## Conteúdos

- create basics tests

# create basics tests

## src/example.spec.ts

```ts
// feature
class FriendList {
  friends = [];

  addFriend(name) {
    this.friends.push(name);
    this.announceFriendship(name);
  }
  announceFriendship(name) {
    console.log(`${name} is now a friend`);
  }
  removeFriend(name) {
    const idx = this.friends.indexOf(name);
    if (idx === -1) {
      throw new Error("Friend not found!");
    }
    this.friends.splice(idx, 1);
  }
}

// tests
describe("FriendList", () => {
  let friendsList;
  beforeEach(() => {
    friendsList = new FriendList();
  });

  it("initiallizes friends lists", () => {
    expect(friendsList.friends.length).toEqual(0);
  });
  it("adds a friend to the list", () => {
    friendsList.addFriend("Glauber");

    expect(friendsList.friends.length).toEqual(1);
  });
  it("announces friendship", () => {
    friendsList.announceFriendship = jest.fn();

    expect(friendsList.announceFriendship).not.toHaveBeenCalled();

    friendsList.addFriend("Glauber");

    expect(friendsList.announceFriendship).toHaveBeenCalledWith("Glauber");
  });

  describe("removeFriend", () => {
    it("removes a friend from the list", () => {
      friendsList.addFriend("Glauber");
      expect(friendsList.friends[0]).toEqual("Glauber");
      friendsList.removeFriend("Glauber");
      expect(friendsList.friends[0]).toBeUndefined();
    });
    it("throws an error as friend does not exist", () => {
      expect(() => friendsList.removeFriend("Glauber")).toThrow(
        new Error("Friend not found!")
      );
    });
  });
});
```
